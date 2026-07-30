---
name: Definition of Read
---
# Definition of Ready

## 1. Terminology & Conformance (RFC-2119)
> [!NOTE]
> The keywords 'MUST', 'MUST NOT', 'REQUIRED', 'SHALL', 'SHALL NOT', 'SHOULD', 'SHOULD NOT', 'RECOMMENDED', 'MAY', and 'OPTIONAL' in this document are to be interpreted as described in BCP 14 [RFC-2119] [RFC-8174].

---

## 2. Mandatory Issue Structure

Every GitHub Issue MUST contain the following sections before being submitted and moved to the "Ready" stage:

### Summary
- **Requirement:** MUST be a single line. SHOULD be prefixed with [{component-name}] (e.g. [warlock-agents]) if known.
- **SSE Context:** Keep it concise. No marketing fluff (e.g. [WBW-10] Expose Definition of Ready as MCP Resource).

### Description
- **Requirement:** MUST contain the subsections below formatted in Markdown.

#### Context & Why
- **Requirement:** MUST state the immediate system problem or need.
- **SSE Context:** Explain how this advances the stability or functionality of the project. Any specific goal dependencies MUST be documented here.

#### Technical Implementation Plan
- **Requirement:** MUST NOT provide full code blocks or exact copy-paste solutions.
- **Requirement:** MUST clearly define the required API surfaces, data contracts, and logical flow/architecture paths. 
- **SSE Context:** Expect a Senior Software Engineer (SSE) will be taking on this ticket. The implementation plan should act as an architectural blueprint or interface contract. The SSE is responsible for the actual code implementation, design pattern selection, and syntax.

#### Acceptance Criteria
- **Requirement:** MUST be a checklist (` - [ ] `). Each item MUST be binary (either it works or it doesn't).
- **SSE Context:** Focus on functional contracts (e.g. ` - [ ] The resource://definitions/ready URI returns the correct Markdown content`).

#### Verification & Testing Instructions
- **Requirement:** MUST provide CLI commands or test inputs.
- **SSE Context:** A senior doesn't guess if code works. These instructions should be able to be executed in local environment for bench testing as well as post-deployment integration testing.

### Scope & Sizing
- **Requirement:** The issue MUST be small enough to be completed within a few days (a single sprint/cycle).
- **SSE Context:** If an issue describes an Epic (e.g., "Refactor Entire Ingestion Pipeline"), it MUST be broken down into smaller, actionable sub-issues before moving to "Ready".

### Architectural Alignment
- **Requirement:** If the issue introduces a new system dependency, infrastructure resource, or major architectural shift, it MUST link to an approved Architectural Decision Record (ADR) in the `wbw-architecture` repository.
- **SSE Context:** Prevents engineers from building large features without design consensus and governance.

### Labels (Tags & Priority)
- **Requirement:** MUST apply standard GitHub labels for categorization (e.g., `Warlock`, `Stability`, `Enhancement`).
- **Requirement:** MUST apply a priority label mirroring our standard levels (`Priority: Minor`, `Priority: Normal`, `Priority: Major`, `Priority: Critical`, `Priority: Show-stopper`).
- **SSE Context:** Enhancement tasks should always have the `Enhancement` label so you can build a clean tracking dashboard in GitHub Projects.

### Milestones
- **Requirement:** SHOULD be assigned to an active GitHub Milestone (e.g., `Project Migration`).
- **SSE Context:** Tracking work against explicit milestones ensures the team is focused on delivering cohesive, bundled value rather than isolated features.

### Dependencies (Cross-Repository)
- **Requirement:** MUST explicitly list any blocking issues, especially across repositories. Use GitHub cross-reference links (e.g., `Depends on Works-by-Worrell/wbw-infra#2`).
- **SSE Context:** With our new decoupled architecture, an application change in `warlock-mcp` frequently requires infrastructure WIF bindings in `wbw-infra`. These cross-boundary dependencies MUST be identified before development begins to avoid blocked pull requests.
