# Agent Use of Delegation and Interaction Traceability (AUDIT) Working Group Charter

Autonomous and semi-autonomous software agents, including those based on LLM-based machine learning systems, are increasingly deployed to act on behalf of users, organizations, and services across the Internet. These agents interact across multiple administrative or trust domains and can initiate actions without direct human oversight at each step.

This introduces challenges for auditability, accountability, and transparency, including:

* Difficulty attributing actions to a specific user, agent instance, or delegation context
* Loss of visibility across long-running or distributed workflows
* Inconsistent capture of delegation relationships, dynamic authorization context, and identity transitions
* Lack of interoperable means to exchange or verify audit-relevant information about the participating agents and their interactions across domains

Effective auditing requires linking user intent to resulting system actions across protocol and administrative boundaries. While traditional workflows support evolving authorization, these transitions are usually explicit and predefined. Agent systems introduce dynamic, fine-grained authorization changes that arise during execution, driven by agent decisions, delegation, and human interaction. Auditing must therefore capture authorization as a time-evolving state and correlate these transitions across interactions and domains.

Additionally, Agent behavior may be non-deterministic and not fully predefined, requiring auditing mechanisms to capture execution context and structure as they emerge. 
Auditing must also distinguish between user, agent, and service identities, and ensure audit data can be selectively disclosed such that it remains interpretable across systems without shared assumptions.

Further, audit information must be verifiable by a party that trusts neither the agent nor its operator. That property is what separates audit records from most existing log mechanisms.

## Scope and Goals
The AUDIT working group will define interoperable mechanisms for auditing and accountability of Agents and delegated systems across Internet protocols.

The group will focus on architectures, protocol-layer specifications, and data representations that enable systems to record, exchange, and verify audit-relevant information across agent interactions. This includes:

* Enabling attribution of actions to a specific user, agent instance, or delegation context
* Capturing delegation chains, authorization state over time, and identity transitions
* Enabling consistent interpretation and correlation of audit data across domains and across long-running or distributed workflows

The working group will compose existing building blocks for identity (WIMSE), attestation (RATS), authorization (OAuth family), transparency (SCITT), context propagation (e.g. W3C Trace Context or other context identifiers), and conversation containers (vCon), and will define only an architecture including interfaces to and profiles of the auditing components, as well as the additional protocol elements, data models, and best practices needed to make these compose coherently for the agent auditing case.

The working group will not define auditing policies or compliance frameworks, but instead provide the technical building blocks needed to support them.
Further, while the entities of a complex agent or workload system need to be identifiable, this group will not work on new identity primitives but rely on work in other groups or fora.

The working group will treat privacy, confidentiality, selective disclosure and retention constraints as core design considerations.
Mechanisms defined by the working group are expected to support auditability without requiring indiscriminate disclosure of prompts, user content, personal data, or unrelated execution context.

## Deliverables
The AUDIT working group is expected to produce:

1. **Architecture for Autonomous Agent Auditing**
An Informational RFC describing roles, trust relationships, and data flows for interoperable auditing, including the relationship between user-facing and system-facing audit signals. This document might also identify needed protocol extensions. 

2. **Audit Data Models and Semantics**
One or more Standards Track RFC(s) that identify and reuse existing or specify new IETF data models that can represent audit information about agents and delegated systems (e.g., interaction records, references to the identities of participating entities, delegation context, authorization state over time, or action provenance).
If existing data models are identified the RFC(s) might create profiles that scope them to a degree of disclosure that is appropriate for audits.
The group will work on the minimal set of audit information and consider a registry to enable experimentation and fast deployment for additional data models.

3. **Protocol Extensions or Profiles**
One or more Standards Track RFCs specifying profiles of, extensions to, or embodiments into existing IETF protocols (e.g., HTTP headers, OAuth token formats, attestation workflows, or claims sets in other data items) to convey audit-related information.
Whether this work is done in this working group or the respective protocol maintenance group depends on the protocols and needs to be considered on a case by case basis.
The working group may also define protocol-independent data representations intended for use by non-IETF logging, telemetry, or audit systems, while avoiding standardization of those external systems themselves.

4. **Best Practices for Deployment and Operation**
An Informational or BCP document providing guidance for secure, interoperable, and privacy-aware auditing, including correlation across interaction types for different deployment models and trust domains.

## Coordination

Agent deployments already emit telemetry; audit records need to be usable in
this context. The working group will therefore coordinate with other SDOs and
projects working in the telemetry space to reduce the risk of gratuitous
incompatibility, initially and specifically with W3C Trace Context, and with the
OpenTelemetry project on semantic conventions for agent telemetry.

Where an existing, broadly adopted semantic convention already names a concept
that the audit data models need, the working group will reuse that name rather
than define a synonym. Where the working group defines an element that telemetry
systems can carry, it will seek a corresponding semantic convention mapping.