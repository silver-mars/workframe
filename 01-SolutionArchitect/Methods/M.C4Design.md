---
type: method
name: C4 Design
context: SolutionArchitectContext
maturity: M3
status: Active
bindsRole: "[R.SolutionArchitect](01-SolutionArchitect/Roles/R.SolutionArchitect.md)"
rcs:
  - "agency: Predictive"
  - "safety: SC2"
preconditions:
  - Access to system requirements and stakeholder context.
  - Understanding of the target system boundary and constraints.
  - Availability of current architecture, domain, and integration information.
postconditions:
  - System context, container, and component views are produced or updated.
  - Architecture decisions and boundaries are clarified.
  - Stakeholders have a shared understanding of the system structure.
evidence:
  - 
---
# C4 Design as an Architectural Thinking Method
## What it is
This approach uses C4 as a disciplined method for architectural thinking and solution design.
It starts with the system of interest, stakeholder concerns, constraints, and quality goals, and then develops architectural understanding across multiple levels of abstraction.
## Why it matters
Architectural decisions are shaped by the concerns of the stakeholders who use, operate, integrate, govern, and evolve the system.
A good C4-based design process helps turn those concerns into clear system boundaries, responsibility structures, integration decisions, and evolution paths, in line with the perspectives of [ISO/IEC/IEEE 42010](http://www.iso-architecture.org/42010/cm/).
## When to use it
Use this method when a system must be designed, reviewed, modernized, explained, or compared at the architectural level.
It is especially useful when the system has unclear boundaries, multiple stakeholders, significant integration points, operational constraints, or competing solution directions.

Identifying the stakeholders around the system of interest and clarifying their roles in shaping requirements, using, operating, integrating, e

It helps define the system of interest, establish its boundaries, separate internal structure from external dependencies, and present the architecture through views suited to different audiences.
It explains why boundaries are drawn in a particular way, which containers carry operational responsibility, where integration seams and bottlenecks emerge, and which elements are most likely to shape future architectural change.
For that reason, the value of C4 design lies in its ability to support systematic reasoning about decomposition, responsibilities, constraints, and evolvability.
Used well, it becomes a practical method for communication, trade-off analysis, and architectural decision support, helping connect business intent, technical structure, and operational reality.

## Inputs to clarify
Before modeling begins, clarify the following:
- The system of interest.
- The bounded context of the design discussion.
- The relevant stakeholders and their concerns.
- Business goals, constraints, and success criteria.
- Key quality attributes such as scalability, resilience, security, operability, and evolvability.
- External systems, dependencies, and likely change drivers.
## Working principle
- Stakeholder concerns come before structural decomposition.
- System boundaries should be explicit before internal structure is refined.
- Different audiences need different views.
- Architectural descriptions should reveal responsibilities, dependencies, constraints, and likely change pressure.
- C4 diagrams are used to support reasoning and communication, not as an end in themselves.

## Priority of architectural attention
The design effort should focus first on what is most likely to affect architectural viability:
- Boundary ambiguity.
- Responsibility ambiguity.
- High-risk integration.
- Operational fragility.
- Security-sensitive elements.
- Likely scaling bottlenecks.
- Areas of expected future change.
## Solution option framing
Once stakeholder concerns and requirements are classified, do not converge immediately on a single target design.
Instead, develop two or three architecturally viable candidate solutions that differ by their core design idea, such as decomposition strategy, integration style, data ownership model, or operational model.
Each candidate should include a short pre-experimental rationale:
- Why this option could plausibly satisfy the key concern.
- Which quality attributes it is expected to strengthen.
- Which trade-off it introduces.
- Which uncertainties or risks still need validation.
- Under which conditions it should remains viable or be rejected.
## Working workflow


## Example cases
[Security stakeholder in critical infrastructure system](C.SecurityStakeholder.md)