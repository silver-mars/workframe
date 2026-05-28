# C4 Design Case: Security Viewpoint for Critical Information Infrastructure
When **information security** is a first-class stakeholder and the target environment is part of critical information infrastructure, the architectural description should include an explicit security viewpoint covering workload runtime controls.
For Kubernetes-based workloads, this security viewpoint can be expressed through pod- and container-level securityContext settings, with container-level configuration overriding pod defaults where fields overlap.

**Stakeholder**: information security.
**Environment**: critical information infrastructure with strict expectations for workload isolation, privilege restriction, and resilience after compromise.
**Concern**: prevent privilege escalation, reduce writable attack surface, enforce non-root execution, and minimize Linux capabilities.
**Architectural response**: define shared runtime defaults at pod level, apply stricter workload-specific controls at container level, and treat policy enforcement as a separate architectural concern.
### Example: workload-level implementation of the runtime security baseline
At manifest level, this policy is expressed through securityContext settings, while enforcement and consistency belong to the wider platform governance model.
```yaml
securityContext:
  capabilities:
    drop:
      - ALL
  runAsUser: 1001
  runAsGroup: 2000
  runAsNonRoot: true
  readOnlyRootFilesystem: true
  allowPrivilegeEscalation: false
  seccompProfile:
    type: RuntimeDefault
```
At system level, these settings should be reinforced by admission controls and platform policies so that the baseline remains enforceable across workloads rather than depending on local developer discipline.

This baseline also changes how the workload is built, tested, debugged, and operated.eams must assume non-root execution, a read-only file system, limited capabilities, and reduced container mutability, so troubleshooting should rely on logs, metrics, traces, crash diagnostics, and controlled debug mechanisms rather than ad-hoc changes inside running containers.