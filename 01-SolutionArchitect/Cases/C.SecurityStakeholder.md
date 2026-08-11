# From Security Concern to UAT Readiness: an architecture case beyond diagrams
This case tracks a direct chain from an abstract security requirement to concrete delivery consequences. Runtime restrictions shaped workload design, manifest preparation, support expectations, and team readiness for user acceptance testing.
## Context
The system under discussion was a Kubernetes-hosted application preparing for user acceptance testing in an environment with strict runtime security expectations.
The delivery scope covered workload packaging, deployment manifest, platform interaction, and operational readiness for development, support, and platform teams.
## How the requirement arrived
Information security was one of the primary stakeholders for this work. The requirement arrived in the abstract form it usually takes: the workload must be hardened, and the environment tolerates no privilege escalation.

When information security is a first-class stakeholder and the target environment is part of critical information infrastructure, the architectural description should include an explicit security viewpoint covering workload runtime controls. I recorded that viewpoint before touching any manifest:

**Stakeholder**: information security.
**Environment**: critical information infrastructure with strict expectations for workload isolation, privilege restriction, and resilience after compromise.
**Concern**: prevent privilege escalation, reduce writable attack surface, enforce non-root execution, and minimize Linux capabilities.
**Architectural response**: define shared runtime defaults at pod level, apply stricter workload-specific controls at container level, and treat policy enforcement as a separate architectural concern.
## From concern to concrete controls
The concern focused on security policies that can be expressed through pod- and container-level settings.
The required baseline covered:
* non-root execution,
* reduced writable surface,
* blocked privilege escalation,
* limited Linux capabilities,
* policy-backed runtime enforcement.

These requirements entered the project as concrete runtime constraints with direct impact on delivery preparation.
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

This moved the topic from a platform configuration detail into an architecture and delivery coordination issue. Runtime hardening shapes more than the deployment manifest: it shapes how workloads are packaged, validated, observed, debugged, supported, and evolved over time. The design problem is to let security controls improve resilience without undermining operability, supportability, or system evolvability.
## Structural view
The repository stores the diagram source as PlantUML and renders the image in GitHub.
```PlantUML
@startuml
skinparam BackgroundColor white
skinparam Shadowing false
skinparam DefaultTextAlignment left
skinparam PackageStyle rectangle
skinparam rectangle {
    RoundCorner 10
}

rectangle "Kubernetes Platform" as K8S {
    rectangle "Application Workload" as APP
}
rectangle "Runtime Policy" as POL

actor "Operations / Support" as OPS

POL --> K8S : constrains runtime
K8S --> APP : hosts workload
OPS --> K8S : operates platform
OPS --> APP : supports workload

note right of APP
Runtime restrictions shape
workload preparation
end note

note bottom of OPS
Support model and troubleshooting
must align before UAT
end note
@enduml
```
This view supported four practical conversations:
* where runtime policy is applied,
* where the platform boundary sits,
* where the application workload runs,
* where operational responsibility changes hands.
## Implementation: pod-level defaults, container-level overrides
The security viewpoint became executable through securityContext settings on two levels: shared defaults at pod level, stricter workload-specific controls at container level, with container-level values taking precedence where fields overlap.
```yaml
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
```
The fragment captured the runtime baseline. The delivery work extended further into image preparation, writable path planning, and support readiness.
## Making the baseline enforceable
At manifest level the policy appears as securityContext settings, but a manifest states an intention rather than guarantees it. At platform level these settings should be reinforced by admission controls and platform policies, so that the baseline remains enforceable across workloads rather than depending on local developer discipline. This is why policy enforcement belongs in the architectural description as a concern of its own, owned by platform governance.
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
## Architectural intervention
The delivery risk lived in operational interpretation and team readiness, not in the diagram. The project needed an additional artifact that translated security constraints into workload preparation, manifest expectations, and support behavior before UAT.

The architectural work covered direct alignment across development, support, and platform participants.
The intervention included:
* surfacing the runtime consequences of the security baseline,
* reviewing workload assumptions against the target execution model,
* checking manifest readiness for the required controls,
* aligning support expectations with the constrained runtime model,
* pushing readiness discussions before the UAT window.

This created a shared engineering interpretation of the security concern.
## Team enablement
A focused enablement track translated the security baseline into concrete engineering actions.
The sessions covered:
* what non-root execution changes in practice,
* how a read-only filesystem affects runtime writes,
* where applications can keep temporary files,
* how logging and diagnostics can work under restricted runtime conditions,
* what support engineers can expect during incident investigation,
* which manifest fields carry the required controls.

This work reduced ambiguity and gave the team a clear basis for preparation.
## Operating under the constraints
The operating model has direct consequences for troubleshooting and support. Teams must work within non-root execution, a read-only file system, limited capabilities, and reduced container mutability. As a result, troubleshooting relies on logs, metrics, traces, crash diagnostics, and controlled debug mechanisms rather than ad-hoc changes inside running containers. Agreeing on this before UAT is what keeps a hardened workload supportable.
## Outcome
The team entered UAT with aligned runtime expectations, prepared manifests, and a support model consistent with the required security baseline.
The project gained delivery stability through earlier interpretation, clearer ownership, and targeted preparation across roles.
## Architectural takeaway
Security concerns can reshape delivery conditions through runtime constraints and team preparation requirements.
Architectural work in such cases includes:
* selecting a useful structural view,
* identifying the operational consequences behind that view,
* creating a translation artifact for the engineers who need it,
* aligning the delivery chain before the final test stage.

This case shows how a stakeholder concern can move through design constraints, team enablement, and delivery preparation into a concrete project outcome.
