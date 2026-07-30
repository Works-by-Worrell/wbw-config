# Works-by-Worrell: Public GitOps Configuration (`wbw-config`)

This repository serves as the public GitOps declaration source for agent personas, user profiles, platform resources, and skill metadata across the **Works-by-Worrell (WBW)** platform.

---

## 1. Directory Layout & Taxonomy

The configuration profiles are structured into specialized directories that correspond to Firestore target collections:

```
wbw-config/
├── .githooks/            # Shared, version-controlled git validation hooks
│   └── commit-msg        # Enforces Conventional Commit standards with issue tags
├── .github/              # CI/CD GitOps pipelines
│   └── workflows/
│       └── sync.yml      # Syncs config changes directly to Firestore
├── agents/               # Markdown Agent Personas (Firestore: agent_configurations)
│   └── warlock.md        # Warlock core agent system prompt & rules
├── profiles/             # Markdown User Profiles (Firestore: user_profiles)
│   └── raworre.md        # Developer profile configuration metadata
├── resources/            # System Markdown Resources (Firestore: system_resources)
│   └── READY.md          # Shared process boundary definitions
└── skills/               # Skill Metadata Documentation (Firestore: skill_metadata)
    └── skill_guide.md    # Actionable capabilities and helper schemas
```

---

## 2. Environment-Aware GitOps Synchronizer

This repository runs a GitHub Actions pipeline (`.github/workflows/sync.yml`) that automates database updates on main-branch merges.

### GitOps Sync Workflow
1.  **Impersonation & Auth:** Authenticates to Google Cloud via Workload Identity Federation (WIF), assuming the GitOps syncer service account identity.
2.  **Pull Syncer Container:** Pulls the pinned `warlock-mcp-syncer` OCI image from the Artifact Registry.
3.  **Validate & Ingest:** Runs pre-sync Pydantic schema validation. If valid, the syncer ingests all markdown frontmatter, calculates MD5 hashes to prevent duplicate database writes (delta-syncing), and writes updates to Firestore.
4.  **Traceability Mapping:** The workflow passes the current Git short-SHA (e.g. `a1b2c3d`) to the sync CLI, which injects it into every database document as `_version_hash` for auditing.
5.  **Environment Isolation:**
    *   Branches targeting `main` merge events deploy to the non-production (`worksbyworrell-nprd`) project.
    *   Automated sync to production is deferred until the production environment is provisioned.
