# From Security Concern to UAT readiness: an architecture case beyond diagrams
## Context
This case covers a Kubernetes-hosted application preparing for user acceptance testing in an environment with strict runtime security expectations.
The delivery scope included workload deployment, manifest preparation, and operational readiness for support and platform teams.
## Stakeholder concern
Information security set one of the primary concern for this case.
The concern focused on security policies, that can be expressed through pod- and container-level settings, such as non-root execution, writable surface reduction, privilege restriction, capability minimization, and enforceable runtime controls.
## Architectural impact
These constraints influenced packaging decisions, startup assumptions, writable path handling, logging strategy, debugging approach, and support procedures.
## Architectural view used
A structural view helped frame the system boundary, the Kubernetes platform boundary, the workload position, and the responsibility split between application and platform layers.
This view supported stakeholder communication and responsibility mapping.




When **information security** is a first-class stakeholder and the target environment is part of critical information infrastructure, the architectural description should include an explicit security viewpoint covering workload runtime controls.
For Kubernetes-based workloads, this security viewpoint can be expressed through pod- and container-level securityContext settings, with container-level values taking precedence where fields overlap.

**Stakeholder**: information security.
**Environment**: critical information infrastructure with strict expectations for workload isolation, privilege restriction, and resilience after compromise.
**Concern**: prevent privilege escalation, reduce writable attack surface, enforce non-root execution, and minimize Linux capabilities.
**Architectural response**: define shared runtime defaults at pod level, apply stricter workload-specific controls at container level, and treat policy enforcement as a separate architectural concern.
### Architectural implications
Runtime hardening must shape more than the deployment manifest. It must also shape how workloads are packaged, validated, observed, debugged, supported, and evolved over time, so that security controls improve resilience without undermining operability, supportability, or system evolvability.
### Example: workload-level implementation of the runtime security baseline
At manifest level, this policy appears as securityContext settings, while platform governance is responsible for enforcing it consistently across workloads.
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
At platform level, these settings should be reinforced by admission controls and platform policies so that the baseline remains enforceable across workloads rather than depending on local developer discipline.

This operating model has direct consequences for troubleshooting and support. Teams must work within non-root execution, a read-only file system, limited capabilities, and reduced container mutability. As a result, troubleshooting should rely on logs, metrics, traces, crash diagnostics, and controlled debug mechanisms rather than ad-hoc changes inside running containers.