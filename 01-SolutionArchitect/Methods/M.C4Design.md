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
This approach uses C4 as a method for architectural thinking and solution design.
It starts with the system of interest, stakeholder concerns, constraints, and quality goals, and then develops architectural understanding across multiple levels of abstraction.
## Why it matters
Architectural decisions are shaped by the concerns of the stakeholders who use, operate, integrate, govern, and evolve the system.
C4 provides a practical structural language for that work and supports [ISO/IEC/IEEE 42010](http://www.iso-architecture.org/42010/cm/)style separation of concerns, viewpoints, and views.
It supports systematic reasoning about decomposition, responsibilities, constraints, and evolvability, making it a practical method for communication, trade-off analysis, and architectural decision support.
## When to use it
Use this method to design, review, modernize, explain, or compare a system when its boundaries, integrations, responsibilities, operational constraints, or solution directions are unclear.
## Inputs to clarify
Before modeling begins, clarify the following:
- The system of interest.
- The bounded context of the design discussion.
- The relevant stakeholders and their concerns.
- Business goals, constraints, and success criteria.
- Key quality attributes such as scalability, resilience, security, operability, and evolvability.
- External dependencies, integrations, and likely change drivers
## Working principles
- Start from stakeholder concerns, then make system boundaries explicit before refining internal structure.
- Use views to reveal responsibilities, dependencies, constraints, change pressure, and high-risk areas.
- Design attention should focus first on boundary ambiguity, responsibility ambiguity, high-risk integrations, operational fragility, scaling bottlenecks, and likely change areas.
- Treat C4 diagrams as reasoning and communication aids, not as architecture itself or as evidence that a design is adequate.
* Explore viable alternatives before convergence when the design space is materially open.
## What C4 explains well
C4 is 
It explains system boundaries, external dependencies, major execution units, responsibility allocation, and where important integration seams exist.
It is especially useful, when you need to show how a system is decomposed, where a key decision sits, which containers carry operational responsibility, and which parts are likely to change independently.
Used this way, C4 makes architectural scope and decomposition discussable before implementation details take over the conversation.
## What C4 does not explain well
C4 is not a complete language for architecture. By itself, it does not explain sequencing, runtime control flow, temporal behavior, failover paths, retry logic, operational procedures, or decision timing very well.
A container view can show that two systems interact, but it usually does not show the exact order of calls, the control conditions, or how behavior changes during provisioning, incident response, recovery, or 
For that reason, C4 cannot be treated as a substitute for dynamic, operational, or decision-flow artifacts. 
## When to add another artifact
Add the smallest complementary artifact that answers the question the structural view leaves open:
- Sequence or flow diagram for interaction order and control flow
- ADR for decision rationale and trade-offs
- Deployment or operational view for runtime placement, ownership, and failure domains
- State or lifecycle artifact for modes and transitions over time
The purpose is to avoid treating a clear structural picture as a complete architectural explanation.
## Solution option framing
Before selecting a target design, develop two or three viable options when they differ materially in decomposition, integration style, data ownership, or operational model.
For each option, record:
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
Check what the current view explains, what it hides, and whether another artifact is needed.
10. **Converge on a target solution**
Approve, combine, narrow, or reject candidate solutions based on architectural fit, trade-offs, and remaining uncertainty.
## Outputs
- A clear definition of the system of interest.
- A stakeholder-aware architectural framing.
- A bounded architectural context.
- Two or three candidate solution directions when the design space is still open.
- Context, container, and selective component views.
- A clearer understanding of responsibilities, dependencies, bottlenecks, and likely evolution paths.
- Explicit limits of each view and complementary artifacts where needed
* A reasoned basis for further design, ADRs, validation, or implementation planning.
## Example cases
[Security stakeholder in critical infrastructure system](C.SecurityStakeholder.md) - illustrated how a stakeholder concern changes boundary decisions and the interpretation of structural views.