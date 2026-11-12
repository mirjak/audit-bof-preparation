# Agent Use of Delegation and Interaction Traceability (AUDIT) Working Group Charter

Autonomous and semi-autonomous software agents, including those based on LLM techniques, are increasingly deployed to act on behalf of users, organizations, and services across the Internet.
These agents interact across multiple administrative or trust domains and can initiate actions without direct human oversight at each step.

This introduces challenges for auditability, accountability, and transparency, including:

* Difficulty attributing actions to a specific user, agent instance, or delegation context
* Loss of visibility across long-running or distributed workflows
* Inconsistent capture of delegation relationships, dynamic authorization context, and identity transitions
* Lack of interoperable means to exchange or verify audit-relevant information about the participating agents and their interactions across domains

To support governance, compliance, transparency, and trust in such environments, auditing is required that collects and correlates evidence across participating domains rather than relying solely on local agent logs, where no single party has complete visibility into a multi-domain interaction.
The scope of such auditing is the observable behavior of agents, including user intent declarations, agent or tool interactions, invoked or declined actions, exchanged data, and resulting outcomes across trust boundaries, but not the auditing of the underlying AI model, training data, or inference mechanisms.

The initial scope of the work will focus on post-hoc auditing.
This means that audit records, whether created and collected during the agent interaction or even before an action takes effect, are evaluated after the fact. 
Audit records may also be used for real-time enforcement, but any specific requirements for this use case may only be considered after re-charter.

Cross-domain agent auditing over the whole action chain, including subagents or tool calls in other domains, requires interoperable communication and records containing an identifier scoped to the interaction to link user intent declarations to resulting system actions across protocol and administrative boundaries.
While traditional workflows support evolving authorization, these transitions are usually explicit and predefined. This work is particularly scoped to agent systems as those introduce dynamic, fine-grained authorization changes that arise during execution, driven by agent decisions, delegation, and human interaction.
Auditing must therefore capture authorization as a time-evolving state and correlate these transitions across interactions and domains while also preserving user privacy.

Additionally, agent behavior may be non-deterministic and not fully predefined, requiring auditing mechanisms to capture execution context and structure as they emerge. 
Auditing must also distinguish between user, agent, and service identities, and ensure audit data can be selectively disclosed such that it remains interpretable across systems without shared assumptions.

Further, audit information, and its integrity, must be verifiable by a party that trusts neither the agent nor its operator. That property is what separates audit records from most existing log mechanisms.

## Scope and Goals

The AUDIT working group will define interoperable mechanisms for auditing and accountability of agents and delegated systems across Internet protocols, enabling the collection and correlation of different kinds of audit records for trusted, potentially third-party, auditing of the full agent interaction chain while keeping privacy consideration as a first priority.

The group will address the mechanisms enabling systems to record, exchange, and verify audit-relevant information across all interactions in a communication chain including the user, one or multiple agents or subagents, and tools.
These mechanisms will include a reference architecture, the necessary data representations, and the extensions or adaptations to existing communication protocols for inter-domain correlation. This includes:

* Enabling attribution of actions to a specific user, agent instance, or delegation context by extending or adapting existing identity and authorization mechanisms
* Specify records format for capturing delegation chains, authorization state over time, and identity transitions
* Enabling consistent interpretation and correlation of audit data across domains and across long-running or distributed workflows while preserving user privacy or other sensitive data by extending or adapting existing communication protocols
* Specify mechanisms and protocols to collect, aggregate, verify, and transparently log records, potentially by a third-party, independent auditor

The working group will compose existing building blocks for identity (WIMSE), attestation (RATS), authorization (OAuth family), transparency logging (SCITT), context propagation (W3C Trace Context or other context identifiers), and privacy-protecting profiles of conversation containers (vCon).
The WG will focus on defining the interfaces to and profiles of the auditing components, as well as the additional protocol elements, data models, and best practices needed to integrate them coherently for the agent auditing case.

The working group will not define auditing policies or compliance frameworks, but instead provide the technical building blocks needed to support them.
Further, while the entities of a complex agent or workload system need to be identifiable, this group will not work on new identity primitives but rely on work in other groups or fora.

The working group will treat privacy, confidentiality, selective disclosure and retention constraints as core design considerations.
Mechanisms defined by the working group are expected to support auditability without requiring indiscriminate disclosure of prompts, user content, personal data, or unrelated execution context.

## Out-Of-Scope

* **Auditing of model training**: 
The AUDIT work focuses on auditing agent workload at run time and provide audit records about actions taken by agents.
This may include interactions with the model but not the model training phase that happens before and interaction is initiated.

* **Interactive/real-time reasoning or enforcement of agent behavior**: 
The AUDIT work focuses on post-hoc auditing. Audit records could also be used during the interaction phase and this might not be precluded by the audit work, however, the initial charter focus is on the post-hoc case.

* **How and when to create the records**: 
The AUDIT work is proposed to be is focused on collection and correlation or records in a record-type agnostic way. The concrete auditing use case defines what kind of record is needed and which information needs to be recorded.
The audit work provide provide a way to communicate requirements on what is needed but when and how exactly the record is created and but which entity is out of scope.

* **Requirements on the auditing system itself**: 
While it might be useful to enable a way to communicate requirements of an auditing system on the content and format of records, the actual needs of different auditing use cases vary widely and do not need to be standardized.

* **Session or context management**: 
While records could also be collected in-band with the agent communication, records are created independently of the session state and therefore any work on session or context management is expected to happen in the agentproto working group.

* **Authorization and delegation mechanism or extensions**: 
Capturing authorization state is essential for auditing, however, the authorization process or any needed extension to the authorization process are not in scope the for AUDIT group. This work is likely to happen in the OATH working group.


## Deliverables
The AUDIT working group is expected to produce:

1. **Architecture for Autonomous Agent Auditing**
An Informational RFC describing roles, trust relationships, and data flows for interoperable auditing, including the relationship between inter-domain audit entities and signals. This document might also identify needed protocol extensions and describe verification processes and requirements, including their limitations. This may include e.g. the need for profiling SCITT or describing how to register an audit record with a SCITT Transparency Service.

2. **Audit Data Models and Semantics**
One or more Standards Track RFC(s) that identify and reuse existing or specify new IETF data models that can represent audit information about agents and delegated systems (e.g., interaction records, references to the identities of participating entities, delegation context, authorization state over time, or action provenance). 
The record format specified in the VCON WG should be considered for auditing and the AUDIT WG should collaborate with the VCON WG on auditing-related requirements on the record format.
This applies in general - if existing data models are identified, the AUDIT working group might create profiles that scope them to a degree of disclosure that is appropriate for audits.
The group will work on the minimal set of audit information and consider a registry to enable experimentation and fast deployment for additional data models.
The working group may also define protocol-independent data representations intended for use by non-IETF logging, telemetry, or audit systems, while avoiding standardization of those external systems themselves.

3. **Protocol Extensions or Profiles**
One or more Standards Track RFCs specifying profiles of, extensions to, or embodiments into existing IETF protocols (e.g., HTTP headers, OAuth token formats, or attestation workflows) to convey audit-related information, reusing the data models from deliverable 2. If possible, AUDIT should (re-)use an existing identifier for record correlation such as to be specified by the agentproto WG.
Whether this work is done in this working group or the respective protocol maintenance group depends on the protocols and needs to be considered on a case by case basis.

5. **Best Practices for Deployment and Operation**
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