\# CCSDS 902.6-B-1 & CSS-SM Space Link Event Sequence Data Format (EVSQ) Specification

\#\# Executive Summary  
This document provides the technical specification and architecture for \*\*EVSQForge Pro\*\*, an industrial aerospace workstation implementing the \*\*Consultative Committee for Space Data Systems (CCSDS) 902.6-B-1\*\* Recommended Standard (\*Cross Support Service Management—Space Link Event Sequence Data Format\*, Blue Book) and \*\*ISO 24128\*\* Cross Support Service Management (CSS-SM).

Following schedule agreement via SSF (CCSDS 902.1-B-1), communications planning via CPIF (CCSDS 902.2-B-1), and RF parameter provisioning via SPDF (CCSDS 902.4-B-1), the \*\*Event Sequence Data Format (EVSQ)\*\* defines the precise, deterministic timeline of actions executed by ground tracking station apertures and spacecraft flight software during a tracking pass.

\#\# 1\. CSS-SM Interoperability Stack & Position of EVSQ  
1\. Service Agreement & Profiles: CCSDS 902.5-B-1 (SACP)  
2\. Communications Planning: CCSDS 902.2-B-1 (CPIF) \[\#482\]  
3\. Simple Schedule Agreement: CCSDS 902.1-B-1 (SSF) \[\#481\]  
4\. Service Package Provisioning: CCSDS 902.4-B-1 (SPDF) \[\#483\]  
5\. Event Sequence Execution: CCSDS 902.6-B-1 (EVSQ) \[\#484\]  
6\. Service Accounting: CCSDS 902.8-B-1 (SMAC)

\#\# 2\. Event Sequence Data Entity Model  
\- Header Metadata: sequenceId, scheduleRef (SSF), packageDataRef (SPDF), customerMission, providerStation, aosTime, losTime.  
\- Chronological Event List: eventId, eventType, criticality (CRITICAL, STANDARD, CONTINGENCY), timingMode (ABSOLUTE, RELATIVE\_TO\_AOS, RELATIVE\_TO\_LOS), offsetSeconds, prerequisites (DAG parent nodes), parameters.

\#\# 3\. Directed Acyclic Graph (DAG) Dependency Rules  
1\. Cycle Prohibition: No event may directly or transitively list itself as a prerequisite.  
2\. Temporal Consistency: Every prerequisite event must resolve to a timestamp equal to or earlier than the dependent event's resolved timestamp.  
3\. Safety Interlocking: FORWARD\_CARRIER\_RADIATE\_ON must strictly precede TELECOMMAND\_MODULATION\_START by \>= 60 seconds to guarantee receiver phase lock.  
4\. Data Integrity Gating: TELEMETRY\_RECORDING\_START must require FRAME\_SYNC\_LOCK.  
