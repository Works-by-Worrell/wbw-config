# Contributing to Works-by-Worrell Public Config (`wbw-config`)

This document outlines the branch taxonomy, commit message standards, and workflows specifically for the **wbw-config** public configuration repository.

---

## 1. Branch Strategy & Taxonomy

All development work MUST occur on a feature or task branch before targeting the `main` branch. All branches MUST align with one of the following prefix categories:

### Branch Prefix Categories
*   `feat/` - Config delivery (e.g. adding new agent personas, editing user profiles, adding skill files)
*   `fix/` - Immediate bug triage, schema corrections, or markdown formatting fixes
*   `test/` - Verification frameworks, mock configurations, and sync pipeline tests
*   `docs/` - Runbook updates, setup guides, and repository README documentation
*   `chore/` - Maintenance, dependency updates, and workspace configuration adjustments

### Branch Naming Convention
All branches MUST follow this format: 
`<type>/issue-<id>-<description>` or `<type>/phase<num>-<short-description>`

**Examples:**
*   `feat/phase5-agent-persona`
*   `fix/issue-2-prompt-typo`
*   `docs/issue-2-readme-sync`

---

## 2. Commit Message Conventions

We strictly adhere to the [Conventional Commits](https://www.conventionalcommits.org/) specification. This enables automated release notes, changelog generation, and clear system auditability.

### Commit Format
Commit messages MUST follow the structure:
```
<type>(<scope>): <short description> (#<issue-number>)

[Optional body explaining design rationale or context]
```
*Note: A git validation hook is configured to enforce that all commit messages end with a parenthesized issue reference (e.g. `(#1)`).*

### Scope Boundaries (Repository Specific)
When writing a commit, the `scope` MUST represent the logical area of this config repository:

| Scope | Logical Domain | Example |
| :--- | :--- | :--- |
| `agent` | Agent system personas and prompt definitions | `feat(agent): add warlock core agent persona (#1)` |
| `prompt` | Prompt text blocks, rules, and instruction overlays | `fix(prompt): correct rule scope in warlock template (#3)` |
| `overlay` | User profile configs and personalized overlays | `feat(overlay): update developer workspace preferences (#1)` |
| `sync` | Sync tool parameters, schemas, and CI/CD pipelines | `infra(sync): configure short-SHA metadata injection (#3)` |
| `gov` | Governance, blueprints, templates, or repository setup | `docs(gov): write readme guidelines for agent layout (#2)` |

---

## 3. Local Git Hook Installation

To enforce these formatting rules locally and prevent commit aborts, you MUST configure your local repository to execute the shared git validation hook:

```bash
git config core.hooksPath .githooks
```
Once configured, the script [.githooks/commit-msg](.githooks/commit-msg) will run automatically before every commit to validate the message format.
