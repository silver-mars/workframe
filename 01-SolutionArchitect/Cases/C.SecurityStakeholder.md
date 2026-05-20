# C4 Design Case: Security Stakeholder in critical information infrastructure
When **information security** is a first-class stakeholder and the target environment is part of critical information infrastructure, the architectural description should include an explicit security viewpoint covering workload runtime controls.
In Kubernetes-based systems one practical implementation of that viewpoint is the use of 

**Stakeholder**: information security.
**Environment**: critical Information infrastructure with elevated requirements for workload isolation, privilege mobilization, and post-compromise resilience.
**Concern**: prevent privilege escalation, reduce writable attack surface, enforce non-root execution, and minimize Linux capabilities.
**Architectural response**: apply a security-focused runtime baseline through spec.containers[\*].securityContext, while keeping pod-level defaults in spec.securityContext where appropriate