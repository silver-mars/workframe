# C4 Design Case: Security Viewpoint for critical information infrastructure
When **information security** is a first-class stakeholder and the target environment is part of critical information infrastructure, the architectural description should include an explicit security viewpoint covering workload runtime controls.
For Kubernetes-based workloads, this security viewpoint can be expressed throught pod- and container-level securityContext settings, with container-level configuration overriding pod defaults where fields overlap.

**Stakeholder**: information security.
**Environment**: critical information infrastructure with strict expectation for workload isolation, privilege escalation  and post-compromise resilience.
**Concern**: prevent privilege escalation, reduce writable attack surface, enforce non-root execution, and minimize Linux capabilities.
**Architectural response**: apply a security-focused runtime baseline through spec.containers[\*].securityContext, while keeping pod-level defaults in spec.securityContext where appropriate.
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
