# Definition of Done (DoD)

## 1. Terminology & Conformance (RFC-2119)
> [!NOTE]
> The keywords 'MUST', 'MUST NOT', 'REQUIRED', 'SHALL', 'SHALL NOT', 'SHOULD', 'SHOULD NOT', 'RECOMMENDED', 'MAY', and 'OPTIONAL' in this document are to be interpreted as described in BCP 14 [RFC-2119] [RFC-8174].

---

## 2. Code & Quality Standards
- **Acceptance Criteria Met:** Every binary checklist item defined in the issue's Definition of Ready MUST be verifiable and pass.
- **Static Analysis:** Code MUST pass all linting, formatting (`.editorconfig`), and type-checking (e.g., `mypy`, `ruff`) without warnings.
- **Clean Code:** The implementation MUST leverage appropriate design patterns (e.g., Repository Pattern, Strategy Pattern) and avoid tightly coupled logic or "god classes."

## 3. Git & Version Control
- **Conventional Commits:** Every commit MUST strictly adhere to the Conventional Commits specification (e.g., `feat:`, `fix:`, `refactor:`).
- **Issue Traceability:** Every commit message MUST end with the exact GitHub Issue reference (e.g., `(#12)`).
- **Clean History:** Feature branches MUST be rebased cleanly against the `main` branch before merging. Merge commits for keeping branches up to date SHOULD NOT be used.

## 4. Testing & Verification
- **Contract Testing:** If an API surface or data contract (e.g., Pydantic schemas) changed, the consuming services MUST be tested against the new contract.
- **Integration & Bench Testing:** The feature MUST be run and verified locally using local sister-directory mounts or mock data prior to deployment.
- **Unit Testing:** New logic paths SHOULD have corresponding automated unit tests.

## 5. CI/CD & Deployment
- **Pipeline Green:** All relevant GitHub Actions workflows (e.g., `sync.yml`, `deploy.yaml`) MUST run to completion successfully.
- **Artifact Generation:** If the change involves application code, the multi-stage Docker build MUST succeed, and an immutable image tag MUST be successfully pushed to the GCP Artifact Registry.
- **Production Verified:** The Cloud Run deployment or GitOps delta-sync MUST execute without downtime or dropped requests.

## 6. Documentation & Architectural Alignment
- **ADR Closure:** If this issue implements an Architectural Decision Record (ADR), that ADR MUST be updated to `Status: Implemented` in the `wbw-architecture` repository.
- **Self-Documenting Code:** Docstrings and inline comments MUST be updated to reflect the new state. Outdated comments MUST be removed.
- **Blueprint Updates:** If the high-level system operation changed, the relevant architectural blueprints MUST be updated.
