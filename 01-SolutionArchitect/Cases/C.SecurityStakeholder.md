# From Security Concern to UAT readiness: an architecture case beyond diagrams
This case tracks a direct chain from security concern to delivery consequence. Runtime restrictions shaped workload design, manifest preparation, support expectations, and team readiness for user acceptance testing.
## Context
The system under discussion was a Kubernetes-hosted application preparing for user acceptance testing in an environment with strict runtime security expectations.
The delivery scope covered workload packaging, deployment manifest, platform interaction, and operational readiness for development, support, and platform teams.
## Security driver
Information security set one of the primary concern for this work.
The concern focused on security policies, that can be expressed through pod- and container-level settings.
The required baseline covered:
* non-root execution,
* reduced writable surface,
* blocked privilege escalation,
* limited Linux capabilities,
* policy-backed runtime enforcement.
These requirements entered the project as concrete runtime constraints with direct impact on delivery preparation (?)
## Architectural impact
The security baseline shaped several parts of the delivery architecture.
It influenced:
* container image assumptions,
* entrypoint and startup behavior,
* writable path handling,
* temporary storage strategy,
* log collection expectations,
* debugging and support routines,
* workload manifest structure.
This moved the topic from a platform configuration detail into an architecture and delivery coordination issues.
## Mini-diagram section
A compact structural view helped frame the main boundaries and responsibility split.
### What this view covers
This view supported four practical conversations:
* where the application sits,
* where the platform boundary sits,
* where runtime policy is applied,
* where operational responsibility changes hands.
### Why an additional artifact was needed
The delivery risk lived in operational interpretation and team readiness.
The project needed an additional artifact that translated security constraints into workload preparation, manifest expectations, and support behavior before UAT.
## Delivery risk
The main risk sat in the gap between accepted constraints and applied engineering behavior.
A team could acknowledge the required runtime baseline during review and still carry incompatible assumptions into:
* container image structure,
* startup logic,
* writable directories,
* support playbooks,
* troubleshooting workflow,
* manifest detail.
That gap could surface late, during integration hardening or UAT preparation.
## Team enablement
A focused enablement track translated the security baseline into concrete engineering actions.
The sessions covered:
* what non-root executions changes in practice,
* how a read-only filesystem affects runtime writes,
* where applications can keep temporary files,
* how logging and diagnostics can work under restricted runtime conditions,
* what support engineers can expect during incident investigation,
* which manifest fields carry the required controls.
This work reduced ambiguity and gave the team a clear preparation.
## Example manifest fragment
The final workload baseline included the following runtime controls:
securityContext:
  runAsNonRoot: true
  runAsUser: 1001
  runAsGroup: 2000
  readOnlyRootFilesystem: true
  allowPrivilegeEscalation: false
  capabilities:
    drop:
      - ALL
  seccompProfile:
    type: RuntimeDefault

The fragment captured the runtime baseline. The delivery work extended further into image preparation, writable path planning, and support readiness.
## Outcome
The team entered UAT with aligned runtime expectations, prepared manifests, and a support model consistent with the required security baseline.
The project gained delivery stability through earlier interpretation, clearer ownership, and targeted preparation across roles.
## Architectural takeaway
Security concerns can reshape delivery conditions through runtime constraints and team preparation requirements.
Architectural work in such cases include:
* selecting a useful structural view,
* identifying the operational consequences behind that view,
* creating a translation artifact for selected engineers,
* aligning the delivery chain before the final test stage.
This case shows how a stakeholder concern can move through design constraints, team enablement, and delivery preparation into a concrete project outcome.


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