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
1. Define the system's criticality class. If there is another important reason to prioritize it, clarify that as well, for example a high-priority feature release requested by the CTO or an emergency cluster update.
This step defines the priority. The priority also depends on the target environment, such as dev, staging, or production. Requests should be classified as current, important or urgent.
In this context, **important** means that the current capacity is insufficient, so you need to estimate when the required capacity will become available.
**Current** means that the quota request is not urgent and the decision can be made later. For example: quota for load testing that will be running only in 3 weeks.

(There are link)




There is a method for cloud capacity planning and quota management