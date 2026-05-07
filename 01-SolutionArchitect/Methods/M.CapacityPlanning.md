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
This approach uses quotas in Openstack, or in another virtualized/cloud environment, to prevent resource exhaustion and maintain sustainable platform capacity.
## Why it matters
Quota management here is a decision framework that helps prioritize requests, reduce unnecessary context switching and ensure that capacity is allocated according to business impact, architectural fit, and actual demand.
## Priority model
Requests should be classified as routine, important or urgent.
* **Routine** means that the request is not time-sensitive, so the decision can be made later. For example, this could be a quota request for load testing scheduled to run in a three weeks.
* **Important** means that current capacity is insufficient, but the situation doesn't require immediate interruption of ongoing work. In this case, you need to estimate when the require capacity will become available or take action to reclaim existing capacity. For example, this may involve running fstrim to reclaim disk space.
* **Urgent** means that the request requires immediate attention and forces you to interrupt your current work. This usually applies to incidents, production-impacting changes, or exceptional high priority deliveries that cannot be delayed.
This classification is needed to reduce context switching. Virtual machines spend time saving their current context and switching to another process, but humans lose much more time when they switch tasks. AI agents also need additional memory to unload the current context and load a new task, so this classification is really about queue management and reducing context-switching overhead.
## Decision workflow
1. Define the critically. 
Define the system's criticality class first. Also identify any additional reason for prioritization, such as production incident, an emergency cluster update, or a high-priority feature release requested by CTO.


This step defines the priority. The priority also depends on the target environment, such as dev, staging, or production. 


3. Ask why they need to increase capacity. What do they want to add to the project? Is it a database, kubernetes cluster or a load balancer? Which goal do they want to achieve? Is the goal to release a new feature or add a new disk for the database? Is the requested quota sufficient, or is it too small or to large? Is this the best solution for their architecture, or can you offer a better one? Clients often don't estimate quota requirements precisely and ask for much more disk space or additional quota just in case.
This step also verifies compliance with cloud-native principles, including scalability, resilience, adaptability automation, etc.


There is a method for cloud capacity planning and quota management