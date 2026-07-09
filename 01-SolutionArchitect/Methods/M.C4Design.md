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
A good C4-based design process helps translate those concerns into clear system boundaries, responsibility structures, integration decisions, and evolution paths, in line with the principles of [ISO/IEC/IEEE 42010](http://www.iso-architecture.org/42010/cm/).
Used well, C4 helps define the system of interest, establish its boundaries, separate internal structure from external dependencies, and present the architecture through views suited to different audiences.
It supports systematic reasoning about decomposition, responsibilities, constraints, and evolvability, making it a practical method for communication, trade-off analysis, and architectural decision support.
## When to use it
Use this method when a system must be designed, reviewed, modernized, explained, or compared at the architectural level.
It is especially useful when the system has unclear boundaries, multiple stakeholders, significant integration points, operational constraints, or competing solution directions.
## Inputs to clarify
Before modeling begins, clarify the following:
- The system of interest.
- The bounded context of the design discussion.
- The relevant stakeholders and their concerns.
- Business goals, constraints, and success criteria.
- Key quality attributes such as scalability, resilience, security, operability, and evolvability.
- External systems, dependencies, and likely change drivers.
## Working principles
- Stakeholder concerns come before structural decomposition.
- System boundaries should be explicit before internal structure is refined.
- Different audiences need different views.
- Architectural descriptions should reveal responsibilities, dependencies, constraints, and likely change pressure.
- Design attention should focus first on boundary ambiguity, responsibility ambiguity, high-risk integrations, operational fragility, scaling bottlenecks, and likely change areas.
- C4 diagrams are used to support reasoning and communication, not as an end in themselves.
## What C4 explains well
C4 strong when the main question is structural.
It helps explains system boundaries, external dependencies, major execution units, responsibility allocation, and where important integration seams exist.
It is especially useful, when 
## Solution option framing
Once stakeholder concerns and requirements are clarified, do not converge immediately on a single target design.
Instead, develop two or three architecturally viable candidate solutions that differ by their core design idea, such as decomposition strategy, integration style, data ownership model, or operational model.
Each candidate should include a short pre-experimental rationale:
- Why this option could plausibly satisfy the key concerns.
- Which quality attributes it is expected to strengthen.
- Which trade-offs it introduces.
- Which uncertainties or risks still need validation.
- Under which conditions it should remain viable or be rejected.
## Design workflow
1. **Define the system of interest**
Clarify what is inside the architecture scope and what belongs to the surrounding environment.
2. **Identify stakeholders and their concerns**
List the stakeholders who shape, use, operate, integrate, govern, or evolve the system, and make their concerns explicit.
3. **Establish architectural boundaries**
Define the system boundary, major external dependencies, upstream and downstream relations, and the main areas of environmental coupling.
4. **Frame candidate solutions**
Develop two or three viable architectural directions before converging on one target design.
5. **Model the context**
Create a context-level view that shows the system of interest, its environment, and the most important interactions.
6. **Model the containers**
Decompose the chosen candidate or compared candidates into major execution, storage, and responsibility-bearing units.
7. **Refine critical components where needed**
Go deeper only where a container carries architectural risk, high complexity, significant coupling, or important decision weight.
8. **Expose operational and integration consequences**
Show where operational responsibility sits, where integration seams exist, where bottlenecks may emerge, and where change pressure is likely to accumulate.
9. **Tailor views to the audience**
Adjust the explanation for sponsors, engineers, operators, security stakeholders, or platform teams without changing the underlying architectural meaning.
10. **Converge on a target solution**
Approve, combine, narrow, or reject candidate solutions based on architectural fit, trade-offs, and remaining uncertainty.
## Outputs
A good run of this method should produce:
- A clear definition of the system of interest.
- A stakeholder-aware architectural framing.
- A bounded architectural context.
- Two or three candidate solution directions when the design space is still open.
- Context, container, and selective component views.
- A clearer understanding of responsibilities, dependencies, bottlenecks, and likely evolution paths.
- A reasoned basis for choosing or rejecting a target solution.
- A bridge to further design work, ADRs, validation activities, or implementation planning.
## Example cases
[Security stakeholder in critical infrastructure system](C.SecurityStakeholder.md)