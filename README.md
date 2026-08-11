Working notes on how I do architecture and DevOps work: the roles I hold, the methods I actually apply, and cases where they met reality.

## Start here

- **[From Security Concern to UAT Readiness](01-SolutionArchitect/Cases/C.SecurityStakeholder.md)** — a real case: how a runtime security baseline on Kubernetes reshaped workload packaging, manifests, and team readiness. Read this to see how I reason from a stakeholder concern to delivery consequences.
- **[C4 Design as an Architectural Thinking Method](01-SolutionArchitect/Methods/M.C4Design.md)** — how I structure architectural reasoning, and why I do *not* draw a component view just to complete the hierarchy.

Five minutes with either file shows you how I work. That is what this repository is for.

## What is here

| Artifact | Count |
|---|---|
| Role definitions (with agency, safety, and justification fields) | 1 — Solution Architect |
| Methods (preconditions, postconditions, scope of use) | 2 — C4 Design, Capacity Planning |
| Cases (concern → architectural impact → delivery outcome) | 1 — Security stakeholder / UAT readiness |

Each artifact carries YAML front matter with a maturity level (M0–M4) and status, so you can tell a settled method from a fresh one.

## Status of this repository

- **What it is:** a working edition, published as a sample of form — not a complete catalogue of my work.
- **Good for:** seeing how I frame a role, write up a method, and trace a case from concern to consequence.
- **Not to be read as:** a full record of my experience, a maturity-measurement system, or evidence of large-scale adoption. Work done under employment agreements is not published here in any form; cases are rewritten to carry the engineering pattern without client-identifying detail.
- **Reviewed:** whenever a new artifact class is added, and at least once a quarter.

## Notes on scope

Client code, internal system names, figures, and commercial terms never appear here. What travels from real work into this repository is the reusable engineering pattern — the failure mode, the constraint, the trade-off — and nothing that identifies where it happened.
