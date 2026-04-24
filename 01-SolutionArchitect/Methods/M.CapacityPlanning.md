---
type: method
name: Capacity planning
context: SolutionArchitectContext
maturity: M3
status: Active
bindsRole: "[R.SolutionArchitect](01-SolutionArchitect/Roles/R.SolutionArchitect.md)"
rcs:
  - "agency: Predictive"
  - "safety: SC2"
preconditions:
  - Access to the infrastructure dashboard
  - Understanding critical system classification
---
# Capacity planning and quota management
## What it is
This approach uses quotas in Openstack, or in another virtualized/cloud environment, to prevent resource exhaustion.

Step by step
1. Define the system's criticality class. Of there is another reason to prioritize it, clarify that as well.
2. If there are an another important reason, ask it (it is a release new important feature for CTO, emergency cluster update, etc.)
This step clauses priority. Works separates to current, important and emergency types. (There are link)



There is a method for cloud capacity planning and quota management