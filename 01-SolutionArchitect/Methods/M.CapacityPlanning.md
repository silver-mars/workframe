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
**Urgent** means that you have to switch context from your current activity and respond to the incident immediately. A high-priority feature release can also be treated as urgent.
This classification is needed to reduce context switching. Virtual machines spend time saving their current context and switching to another process, but humans lose much more time when they switch tasks. AI agents also need additional memory to unload the current context and load a new task, so this classification is really about queue management and reducing context-switching overhead.
2. Ask why they need to increase capacity. What do they want to add to the project? Is it a database, kubernetes cluster or a load balancer? Which goal do they want to achieve? Is the goal to release a new feature or add a new disk for the database? Is the requested quota sufficient, or is it too small or to large? Is this the best solution for their architecture, or can you offer a better one? Clients often don't estimate quota requirements precisely and ask for much more disk space or additional quota just in case.
This step also verifies compliance with cloud-native principles, including scalability, resilience, adaptability


There is a method for cloud capacity planning and quota management