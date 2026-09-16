# Name: Agent Use of Delegation and Interaction Traceability (AUDIT)

# Description
Autonomous and semi-autonomous software agents are increasingly acting on behalf of users across multiple services and administrative domains. The increased use of complex agent communications introduces significant challenges for auditability and accountability. Existing mechanisms, such as system logs, tracing systems, and authorization frameworks, capture individual aspects of system behavior but lack interoperable support for correlating user intent, delegation chains, authorization state, and resulting actions across domains. This creates challenges for fundamental questions required for compliance, operational debugging, and user trust, such as who initiated an action, under which authority it occurred, and how permissions evolved during execution.

The AUDIT effort aims to define interoperable protocol mechanisms and data models to enable auditing of complex, distributed, and time-evolving systems. This includes an architectural concept, common models for audit records, propagation of audit context across interactions, and integration with existing IETF protocols such as OAuth, HTTP, and attestation and transparency frameworks.

# Required Details

Status: WG forming (proposed chairs: Yaroslav Rosomakho)
Responsible AD: SEC ADs
BOF proponents: Mirja Kühlewind <mirja.kuehlewind@ericsson.com>, Henk Birkholz <henk.birkholz@ietf.contact>, Pam Dingle <Pamela.Dingle@microsoft.com>
Number of people expected to attend: 100
Length of session (1 or usually 2 hours): 1.5-2 hours
Conflicts (whole Areas and/or WGs)
Chair Conflicts: TBD
Technology Overlap: OAUTH, WIMSE, SCITT, RATS, HTTPbis, Webbotauth
Key Participant Conflict: SPICE, IOTops, SCONE, MASQUE, QUIC, MAPRG, probably more...

# Information for IAB/IESG

Any protocols or practices that already exist in this space:

OAuth 2.0 (Token Exchange for delegated authorization)
SCITT (transparency service)
RATS (remote attestation)
HTTP and W3C Trace Context (request correlation and propagation)
vCon (conversation record format)
WIMSE (workload identifiers)
Which (if any) modifications to existing protocols or practices are required:

Profiles for RATS and SCITT
Extensions to HTTP (conext header) and potentially oauth (conext in tokens)
Which (if any) entirely new protocols or practices are required:

Data model for records
Open source projects (if any) implementing this work:

Implementers who responded to the question in issue #9 of this repository:

- Agent Passport System (APS), Apache-2.0, draft-pidlisnyi-aps. Published on npm and PyPI, with a conformance suite of canonical-JSON fixtures that a verifier in any language can check for byte-parity.
- Agent Action Capsule, Apache-2.0 and BSD-3, draft-mih-scitt-agent-action-capsule. Reference implementations in Python and Go, 32 frozen conformance vectors, and producer adapters for eight agent frameworks.
- Vaara, AGPL-3.0, draft-sirkkavaara-vaara-receipt. Released on PyPI and npm, with 50 conformance suites whose checkers import no Vaara code and recompute each verdict from its own case files.

Potentially also logging frameworks like OpenTelemetry (TBD)

# Agenda
Intro and Motivation (10 mins)
Architecture overview und use cases (20 mins)
Relation to other IETF work (10 mins)
Review of proposed charter and discussion (45 mins)

# Links to the mailing list, draft charter if any (for WG-forming BoF), relevant Internet-Drafts, etc.

Mailing List: Initial discussion on agent2agent@ietf.org list, also announced on oauth, wimse, scitt, and rats
Draft charter: https://github.com/mirjak/audit-bof-preparation/blob/main/audit-charter.md
Relevant Internet-Drafts:
Architecture:
https://www.ietf.org/archive/id/draft-kuehlewind-audit-architecture-00.html
Solutions:
Verifiable Agent Conversation Records: https://www.ietf.org/archive/id/draft-birkholz-verifiable-agent-conversations-00.html
