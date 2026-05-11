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
This approach uses quotas in OpenStack, VMware, or in another virtualized/cloud environment, to prevent resource exhaustion and maintain sustainable platform capacity.
## Why it matters
Quota management here is a decision framework that helps prioritize requests, reduce unnecessary context switching and ensure that capacity is allocated according to business impact, architectural fit, and actual demand.
## Priority model
Requests should be classified as routine, important or urgent.
* **Routine** means that the request is not time-sensitive, so the decision can be made later. For example, this could be a quota request for load testing scheduled to run in three weeks.
* **Important** means that current capacity is insufficient, but the situation doesn't require immediate interruption of ongoing work. In this case, you need to estimate when the required capacity will become available or take action to reclaim existing capacity. For example, this may involve running fstrim to reclaim disk space.
* **Urgent** means that the request requires immediate attention and forces you to interrupt your current work. This usually applies to incidents, production-impacting changes, or exceptional high priority deliveries that cannot be delayed.
This classification is needed to reduce context switching. Virtual machines spend time saving their current context and switching to another process, but humans lose much more time when they switch tasks. AI agents also need additional memory to unload the current context and load a new task, so this classification is really about queue management and reducing context-switching overhead.
## Decision workflow
1. **Define the criticality**
Define the system's criticality class first. The priority also depends on the target environment, such as development, staging, or production, because the same request may be treated differently depending on where the workload runs.
Also identify any additional reason for prioritization, such as a production incident, an emergency cluster update, or a high-priority feature release requested by the CTO.
2. **Clarify the purpose**
Ask why additional capacity is needed. Identify what the teams want to add or change, such as a database, a Kubernetes cluster, a load balancer or additional storage. Then clarify the expected outcome, for example a new feature release, higher traffic tolerance, better database performance, or platform stabilization.
3. **Review current capacity**
Check current utilization, forecast growth, available regional capacity, and quota headroom. This step should confirm whether the request is driven by actual demand, projected growth, or inefficient resource usage.
4. **Assess the architecture**
Evaluate whether the request is architecturally appropriate and aligned with cloud-native principles, including scalability, resilience, adaptability, and automation. A quota increase should not be the default answer if a better architectural solution is available.
5. **Validate right-sizing**
Determine whether the requested quota is properly sized. In many cases, clients often overestimate their needs and ask for extra disk space or other quotas just in case. The request should be large enough to support the target workload, but not oversized without evidence.
6. **Make the decision**
Based on the findings, decide whether to approve, adjust, delay, reject, or replace the request with a better solution. The goal is to satisfy the request, preserve platform stability and allocate capacity responsibly.