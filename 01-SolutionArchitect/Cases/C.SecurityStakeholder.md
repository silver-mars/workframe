# C4 Design Case: Security Viewpoint for critical information infrastructure
When **information security** is a first-class stakeholder and the target environment is part of critical information infrastructure, the architectural description should include an explicit security viewpoint covering workload runtime controls.
For Kubernetes-based workloads, this security viewpoint can be expressed throught pod- and container-level securityContext settings, with container-level configuration overriding pod defaults where fields overlap.

**Stakeholder**: information security.
**Environment**: critical information infrastructure with strict expectation for workload isolation, privilege restriction, and resilience after compromise.
**Concern**: prevent privilege escalation, reduce writable attack surface, enforce non-root execution, and minimize Linux capabilities.
**Architectural response**: keep shared runtime defaults at pod level, place stricter workload-specific controls at container level and treat policy enforcement as a separate architectural concern.
### Example snippet
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

This baseline also changes how the workload built, tested, debugged, and operated: team must assume non-root execution, a read-only file system, limited capabilities, and reduced container mutability, so troubleshooting should rely on logs, metrics, traces, crash diagnostics, 