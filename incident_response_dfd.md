# Incident Response System - Data Flow Diagram

## Level 0 Context Diagram

```
                    INCIDENT RESPONSE SYSTEM
                         CONTEXT DIAGRAM
    ═══════════════════════════════════════════════════════════════

                           [USER]
                             │
                      1. Submit Incident
                             ▼
    ┌─────────────────────────────────────────────────────────────┐
    │                                                             │
    │                INCIDENT RESPONSE SYSTEM                     │
    │                                                             │
    │    • Incident Detection & Processing                        │
    │    • Alert Management                                       │
    │    • Case Management                                        │
    │    • Forensic Analysis                                      │
    │    • Recovery Operations                                    │
    │                                                             │
    └─────────────────┬───────────────────┬───────────────────────┘
                      │                   │
              3. Alert│                   │6. Store Data
                      ▼                   ▼
            [NOTIFICATION]            [DATABASE]
                SYSTEM                 STORAGE
                      ▲                   ▲
                      │                   │
              4. Status Update    2. Query/Update
                      │                   │
                   [IT STAFF]◄────────────┘
                      │
                5. Resolve Incident
                      │
                      ▼
              [EXTERNAL SYSTEMS]
```

## Level 1 Process Flow Diagram

```
                    INCIDENT RESPONSE SYSTEM
                        PROCESS FLOW (LEVEL 1)
    ═══════════════════════════════════════════════════════════════

    [USER]
      │
      │ 1.1 Submit Report
      ▼
┌─────────────┐    1.2 Create Ticket    ┌─────────────┐
│   REPORT    │─────────────────────────▶│ TICKET DB   │
│  INCIDENT   │                         │   (D1)      │
└─────────────┘                         └─────────────┘
      │                                       ▲
      │ 1.3 Raw Data                          │
      ▼                                       │ 2.2 Update Status
┌─────────────┐    2.1 Analyzed Data    ┌─────────────┐
│   DETECT    │─────────────────────────▶│   TRIAGE    │
│ & ANALYZE   │                         │  PROCESS    │
└─────────────┘                         └─────────────┘
      ▲                                       │
      │ 2.3 Feedback                          │ 3.1 Containment Plan
      │                                       ▼
      │                                 ┌─────────────┐
      │                                 │   CONTAIN   │
      │                                 │  INCIDENT   │
      │                                 └─────────────┘
      │                                       │
      │                                       │ 3.2 Evidence
      │                                       ▼
      │                                 ┌─────────────┐
      │                                 │ FORENSICS   │
      │                                 │  ANALYSIS   │
      │                                 └─────────────┘
      │                                       │
      │                                       │ 4.1 Analysis Results
      │                                       ▼
      │                                 ┌─────────────┐
      │                                 │ ERADICATE   │
      │                                 │   THREAT    │
      │                                 └─────────────┘
      │                                       │
      │                                       │ 5.1 Clean System
      │                                       ▼
      │                                 ┌─────────────┐
      │ 6.1 Lessons Learned             │   RECOVER   │
      └─────────────────────────────────│   SYSTEM    │
                                        └─────────────┘
                                              │
                    ┌─────────────────────────┼─────────────────────────┐
                    │ 5.2 Recovery Data       │ 5.3 Archive Data        │
                    ▼                         ▼                         ▼
              ┌─────────────┐           ┌─────────────┐         ┌─────────────┐
              │ KNOWLEDGE   │           │    USER     │         │ ARCHIVE DB  │
              │   BASE      │           │  NOTIFICATION│         │    (D2)     │
              │   (D3)      │           │             │         │             │
              └─────────────┘           └─────────────┘         └─────────────┘
                    ▲                         ▲
                    │                         │
                    │ 6.2 Query Knowledge     │ 7.1 Status Updates
                    │                         │
                   [IT STAFF]─────────────────┘
```

## Data Stores

| ID | Name | Description |
|----|------|-------------|
| D1 | TICKET DB | Stores incident tickets, status, and metadata |
| D2 | ARCHIVE DB | Long-term storage of resolved incidents |
| D3 | KNOWLEDGE BASE | Stores lessons learned, procedures, and best practices |

## External Entities

| Entity | Description |
|--------|-------------|
| USER | End users who report incidents |
| IT STAFF | IT personnel who manage and resolve incidents |
| NOTIFICATION SYSTEM | External alerting and notification services |
| EXTERNAL SYSTEMS | Third-party tools and systems involved in incident response |

## Process Descriptions

### Level 0 Processes
1. **Submit Incident** - Users report security incidents or system issues
2. **Query/Update** - IT staff access and update incident information
3. **Alert** - System sends notifications about critical incidents
4. **Status Update** - IT staff receive updates on incident progress
5. **Resolve Incident** - IT staff take action to resolve incidents
6. **Store Data** - System stores incident data and resolution information

### Level 1 Processes
1. **Report Incident** - Initial incident reporting and ticket creation
2. **Detect & Analyze** - Automated and manual analysis of incidents
3. **Triage Process** - Priority assessment and resource allocation
4. **Contain Incident** - Immediate containment actions
5. **Forensics Analysis** - Detailed investigation and evidence collection
6. **Eradicate Threat** - Remove the root cause of the incident
7. **Recover System** - Restore normal operations and services

## Data Flows

### Primary Data Flows
- **Incident Reports**: User → System (incident details, timestamps, impact)
- **Alert Notifications**: System → IT Staff (severity, type, affected systems)
- **Status Updates**: System → User/IT Staff (progress, resolution status)
- **Forensic Evidence**: System → Archive (logs, analysis results, artifacts)
- **Knowledge Updates**: System → Knowledge Base (lessons learned, procedures)

### Supporting Data Flows
- **Query Responses**: Database → System (historical data, patterns)
- **Configuration Data**: IT Staff → System (policies, thresholds, procedures)
- **Reporting Data**: System → Management (metrics, trends, compliance)