# Agent Use of Delegation and Interaction Traceability (AUDIT) Working Group Charter

Autonomous and semi-autonomous software agents, including those based on LLM techniques, are increasingly deployed to act on behalf of users, organizations, and services across the Internet. These agents interact across multiple administrative or trust domains and can initiate actions without direct human oversight at each step.

This introduces challenges for auditability, accountability, and transparency, including:

* Difficulty attributing actions to a specific user, agent instance, or delegation context
* Loss of visibility across long-running or distributed workflows
* Inconsistent capture of delegation relationships, dynamic authorization context, and identity transitions
* Lack of interoperable means to exchange or verify audit-relevant information about the participating agents and their interactions across domains

To support governance, compliance, transparency, and trust in such environments, auditing is required that collects and correlates evidence across participating domains rather than relying solely on local agent logs, where no single party has complete visibility into a multi-domain interaction. The scope of such auditing is the observable behavior of agents, including user intent declarations, agent or tool interactions, invoked or declined actions, exchanged data, and resulting outcomes across trust boundaries, but not the auditing of the underlying AI model, training data, or inference mechanisms.

Cross-domain agent auditing over the whole action chain, including subagents or tool calls in other domains, requires interoperable communication and records containing a common identifier to link user intent declarations to resulting system actions across protocol and administrative boundaries.
While traditional workflows support evolving authorization, these transitions are usually explicit and predefined. This work is particularly scoped to agent systems as those introduce dynamic, fine-grained authorization changes that arise during execution, driven by agent decisions, delegation, and human interaction.
Auditing must therefore capture authorization as a time-evolving state and correlate these transitions across interactions and domains while also preserving user privacy.

Additionally, agent behavior may be non-deterministic and not fully predefined, requiring auditing mechanisms to capture execution context and structure as they emerge. 
Auditing must also distinguish between user, agent, and service identities, and ensure audit data can be selectively disclosed such that it remains interpretable across systems without shared assumptions.

Further, audit information must be verifiable by a party that trusts neither the agent nor its operator. That property is what separates audit records from most existing log mechanisms.

## Scope and Goals

The AUDIT working group will define interoperable mechanisms for auditing and accountability of agents and delegated systems across Internet protocols, enabling the collection and correlation of different kinds of audit records for trusted, potentially third-party, auditing of the full agent interaction chain while keeping privacy consideration as a first priority.

The group will address the mechanisms enabling systems to record, exchange, and verify audit-relevant information across all interactions in a communication chain including the user, one or multiple agents or subagents, and tools. These mechanisms will include a reference architecture, the necessary data representations, and the extensions or adaptations to existing communication protocols for inter-domain correlation. This includes:

* Enabling attribution of actions to a specific user, agent instance, or delegation context by extending or adapting existing identity and authorization mechanisms
* Specify records format for capturing delegation chains, authorization state over time, and identity transitions
* Enabling consistent interpretation and correlation of audit data across domains and across long-running or distributed workflows while preserving user privacy or other sensitive data by extending or adapting existing communication protocols
* Specify mechanisms and protocols to collect, aggregate, verify, and transparently log records, potentially by a third-party, independent auditor

The working group will compose existing building blocks for identity (WIMSE), attestation (RATS), authorization (OAuth family), transparency logging (SCITT), context propagation (W3C Trace Context or other context identifiers), and privacy-protecting profiles of conversation containers (vCon). The WG will focus on defining the interfaces to and profiles of the auditing components, as well as the additional protocol elements, data models, and best practices needed to integrate them coherently for the agent auditing case.

The working group will not define auditing policies or compliance frameworks, but instead provide the technical building blocks needed to support them.
Further, while the entities of a complex agent or workload system need to be identifiable, this group will not work on new identity primitives but rely on work in other groups or fora.

The working group will treat privacy, confidentiality, selective disclosure and retention constraints as core design considerations.
Mechanisms defined by the working group are expected to support auditability without requiring indiscriminate disclosure of prompts, user content, personal data, or unrelated execution context.

## Deliverables
The AUDIT working group is expected to produce:

1. **Architecture for Autonomous Agent Auditing**
An Informational RFC describing roles, trust relationships, and data flows for interoperable auditing, including the relationship between inter-domain audit entities and signals. This document might also identify needed protocol extensions. 

2. **Audit Data Models and Semantics**
One or more Standards Track RFC(s) that identify and reuse existing or specify new IETF data models that can represent audit information about agents and delegated systems (e.g., interaction records, references to the identities of participating entities, delegation context, authorization state over time, or action provenance).
If existing data models are identified the RFC(s) might create profiles that scope them to a degree of disclosure that is appropriate for audits.
The group will work on the minimal set of audit information and consider a registry to enable experimentation and fast deployment for additional data models.
The data models should enable an interaction to be correlated with the authorization and delegation relationship that the record claims.

3. **Protocol Extensions or Profiles**
One or more Standards Track RFCs specifying profiles of, extensions to, or embodiments into existing IETF protocols (e.g., HTTP headers, OAuth token formats, attestation workflows, or claims sets in other data items) to convey audit-related information.
Whether this work is done in this working group or the respective protocol maintenance group depends on the protocols and needs to be considered on a case by case basis.
The working group may also define protocol-independent data representations intended for use by non-IETF logging, telemetry, or audit systems, while avoiding standardization of those external systems themselves.

4. **Best Practices for Deployment and Operation**
An Informational or BCP document providing guidance for secure, interoperable, and privacy-aware auditing, including correlation across interaction types for different deployment models and trust domains.
