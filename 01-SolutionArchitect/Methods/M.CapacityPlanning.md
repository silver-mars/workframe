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
This step defines the priority. The priority also depends on the target environment, such as dev, staging, or production. Requests should be classified as routine, important or urgent.
In this context, **important** means that the current capacity is insufficient, so you need to estimate when the required capacity will become available, or take action to reclaim existing capacity. For example, this may involve running fstrim to reclaim disk space.
**Routine** means that the quota request is not urgent, so the decision can be made later. For example, this could be a quota request for load testing that is scheduled to run in three weeks.
**Urgent** means that you have to switch context from your current activity and respond to the incident immediately. A high-priority feature release i
This classification need for less switch context:
virtual machines lose nanoseconds for save their current context and switch to an another process, but human lose more time, AI agents also need more memory to free up current quests and load a new task, so this is about stack (or очередь) and context switching manage.

(There are link)




There is a method for cloud capacity planning and quota management