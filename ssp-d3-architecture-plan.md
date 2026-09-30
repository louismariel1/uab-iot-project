Below is the **updated D3 plan**, incorporating the improvements from the comparison and aligned with the frozen D2 and the frozen overall SSP project structure.

 # D3 — Block & Communications Architecture

 **Delivery purpose:** Translate the frozen D2 requirements into the SSP functional, block, and communications architecture.

 > **D2 = What SSP must do and how well it must perform.**\
>  **D3 = Where SSP functions reside, how the blocks are organized, and how they communicate.**\
>  **D4 = Which concrete hardware/software components implement D3.**

 D3 should therefore remain an **architectural design**, not become a component-selection or implementation document.

---

 ## 1\. Introduction and D3 Objectives

 ### 1.1 Purpose of D3

 Define the objective of the Block & Communications Architecture delivery.

 ### 1.2 Relationship with D2

 Explain that the frozen D2 requirements are the architectural input.

 ### 1.3 Architectural design approach

 Establish the progression:

 **D2 Requirements → Functional Decomposition → Blocks → Interfaces → Communications → Selected Architecture**

 ### 1.4 D3 scope and boundaries

 Explicitly define what is included in D3 and what is deferred to later deliveries.

 ### 1.5 D3 deliverables

 The main D3 outputs should be:

 - functional decomposition;
- system block architecture;
- Device/Edge/Cloud/UI allocation;
- communication architecture;
- interface definitions;
- principal data/control flows;
- security and resilience boundaries;
- D2-to-D3 traceability;
- architectural trade-offs;
- final selected architecture.

---

 # 2\. Architectural Requirements and Principles

 This section translates the most important D2 requirements into **architectural constraints**.

 ### 2.1 Distributed processing

 Define why processing is distributed across Device, Edge and Cloud.

 ### 2.2 Device → Edge → Cloud → UI organization

 Establish the principal system chain.

 ### 2.3 Energy-aware operation

 Show how the architecture supports low-power autonomous operation.

 ### 2.4 Event-oriented operation

 Distinguish normal telemetry from higher-priority events.

 ### 2.5 Privacy-aware processing

 Prefer local/edge processing when transmission of raw information is unnecessary.

 ### 2.6 Communication resilience

 The architecture must tolerate temporary communication failures.

 ### 2.7 Local buffering and synchronization

 Define the exist across devices, communication links, cloud services and UI architectural need for local storage and later synchronization.

 ### 2.8 Security by design

 Security must exist across devices, communication links, cloud services and UI.

 ### 2.9 Scalability

 The architecture must support the D2 scalability requirements without requiring a dedicated infrastructure for each deployment.

 ### 2.10 Bidirectional operation

 Support not only:

 **Device → Edge → Cloud → UI**

 but also:

 **UI → Cloud → Edge → Device**

 for configuration, policies, commands and device management.

---

 # 3\. Functional Decomposition

 Before selecting blocks or technologies, define **what SSP functions must exist**.

 ### 3.1 Sensing

 ### 3.2 Sensor acquisition

 ### 3.3 Local preprocessing

 ### 3.4 Event detection

 ### 3.5 Local storage and buffering

 ### 3.6 Device communication

 ### 3.7 Edge data processing

 ### 3.8 Feature extraction

 ### 3.9 Edge AI/inference

 ### 3.10 Cloud ingestion

 ### 3.11 Cloud processing

 ### 3.12 Historical storage

 ### 3.13 Cloud analytics and AI

 ### 3.14 Alert generation

 ### 3.15 Device management

 ### 3.16 User and role management

 ### 3.17 Monitoring and visualization

 ### 3.18 Configuration and control

 ### 3.19 Audit and security management

 ### 3.20 Function-to-layer allocation

 Map every major function to:

 **Device / Edge / Cloud / UI**

 This section should answer:

 > **What does SSP need to do, independently of which particular component or technology performs it?**

---

 # 4\. Overall SSP Block Architecture

 This becomes the first major architectural view.

 ### 4.1 System-level architecture

 ### 4.2 Device layer

 ### 4.3 Edge/Mobile layer

 ### 4.4 Cloud layer

 ### 4.5 User/UI layer

 ### 4.6 Main system block diagram

 The primary conceptual chain should remain:

```
Environment
     │
     ▼
  DEVICE
     │
     │ C1
     ▼
   EDGE
     │
     │ C2
     ▼
  CLOUD
     │
     │ C3
     ▼
    UI
```

 with appropriate reverse control/configuration paths.

 ### 4.7 Functional allocation across layers

 Show which functions are performed in each layer.

---

 # 5\. Device Architecture

 Define the **logical architecture of the SSP device**, without prematurely selecting exact components.

 ### 5.1 Device functional blocks

 ### 5.2 Sensor subsystem

 ### 5.3 Sensor acquisition

 ### 5.4 Local processing

 ### 5.5 Event detection

 ### 5.6 Local storage/buffering

 ### 5.7 Communication subsystem

 ### 5.8 Energy-management subsystem

 ### 5.9 Device security

 ### 5.10 Internal device interfaces

 For each major block describe:

 **Input → Function → Output → Interface**

 For example:

 > Sensor data → local preprocessing → motion features → event-processing subsystem.

---

 # 6\. Edge / Mobile Architecture

 The Edge should be treated as an actual processing layer, not merely as a BLE gateway.

 ### 6.1 Edge functional role

 ### 6.2 Device communication gateway

 ### 6.3 Message validation

 ### 6.4 Data processing

 ### 6.5 Aggregation

 ### 6.6 Feature extraction

 ### 6.7 Event/risk processing

 ### 6.8 Local AI/inference

 ### 6.9 Local buffering

 ### 6.10 Synchronization

 ### 6.11 Device configuration/control

 ### 6.12 Edge security

 ### 6.13 Edge failure behavior

---

 # 7\. Cloud Architecture

 D3 defines the **logical cloud architecture**, without yet committing to specific cloud vendors or services.

 ### 7.1 Cloud functional blocks

 ### 7.2 Data ingestion

 ### 7.3 Data validation

 ### 7.4 Cloud processing

 ### 7.5 Historical storage

 ### 7.6 Analytics

 ### 7.7 AI/model management

 ### 7.8 Device management

 ### 7.9 User and role management

 ### 7.10 APIs

 ### 7.11 Cloud security boundary

 ### 7.12 Cloud scalability

---

 # 8\. User / UI Architecture

 The UI is explicitly represented as the user-facing layer of SSP.

 ### 8.1 UI functional role

 ### 8.2 Monitoring

 ### 8.3 Current status

 ### 8.4 Alerts and notifications

 ### 8.5 Historical information

 ### 8.6 Device status

 ### 8.7 Configuration

 ### 8.8 Administration

 ### 8.9 User/role interaction

 ### 8.10 UI ↔ Cloud interface

---

 # 9\. Communications Architecture

 This is one of the principal sections of D3.

 Define the major communication interfaces before choosing concrete technologies.

 ## 9.1 Communication architecture overview

 ## 9.2 C1 — Device ↔ Edge

 Define:

 - direction;
- purpose;
- expected information;
- latency;
- throughput;
- range;
- energy constraints;
- reliability;
- security;
- candidate technologies.

 D2-derived constraints should be explicitly referenced.

 ## 9.3 C2 — Edge ↔ Cloud

 Define:

 - telemetry;
- events;
- status;
- synchronization;
- configuration;
- commands;
- security;
- connectivity requirements.

 ## 9.4 C3 — Cloud ↔ UI

 Define:

 - monitoring;
- alerts;
- queries;
- historical data;
- configuration;
- administration.

 ## 9.5 Reverse/control communication paths

 Explicitly show:

 **UI → Cloud → Edge → Device**

 ## 9.6 Communication requirements

 Map communication requirements back to D2.

 ## 9.7 Candidate communication technologies

 Evaluate appropriate alternatives.

 ## 9.8 Selected communication architecture

 Present the proposed technology at the architectural level.

---

 # 10\. Communication Interface Contracts

 For each major interface, define a consistent interface specification.

 | Parameter | C1 Device–Edge | C2 Edge–Cloud | C3 Cloud–UI |
| --- | --- | --- | --- |
| Direction | Bidirectional | Bidirectional | Bidirectional |
| Purpose | Device telemetry/events/control | Synchronization/analytics/control | Monitoring/control |
| Main data | Features/events/status | Processed data/events | Status/alerts/history |
| Latency | D2 requirement | D2 requirement | D2/UI requirement |
| Security | Required | Required | Required |
| Buffering | Required | Required | Application dependent |
| Failure handling | Local operation | Local buffering | Reconnection/session handling |

The exact values should come from the frozen D2 rather than being invented in D3.

 For each interface, the general contract is:

 > **Source → Destination → Direction → Purpose → Data → Performance → Security → Failure behavior**

---

 # 11\. Data and Information Flow

 D3 should show **architecturally significant data flows**, while leaving detailed data schemas for the later Data Flow chapter.

 ### 11.1 Normal telemetry flow

 **Sensors → Device processing → summarized information → Edge → Cloud → UI**

 ### 11.2 Event/alert flow

 **Sensor/event → Device → priority event → Edge → processing → Cloud → UI alert**

 ### 11.3 Configuration/control flow

 **UI → Cloud → Edge → Device**

 ### 11.4 Connectivity-loss flow

 **Device → local processing → local buffer → reconnection → synchronization**

 ### 11.5 Privacy-aware information flow

 Show when raw data remains local and when a minimized representation is transmitted.

 ### 11.6 Data ownership across layers

 Identify where data is:

 - generated;
- processed;
- temporarily stored;
- transmitted;
- permanently stored;
- consumed.

 Detailed data types, packet formats, database schema and storage sizing remain for later chapters.

---

 # 12\. Security Architecture

 D3 establishes the **security architecture**, not detailed implementation.

 ### 12.1 Security boundaries

 ### 12.2 Device identity

 ### 12.3 Authentication

 ### 12.4 Authorization

 ### 12.5 Confidentiality

 ### 12.6 Integrity

 ### 12.7 Protected communication

 ### 12.8 Role-based access

 ### 12.9 Auditability

 ### 12.10 Security management path

 The architecture should show:

 **Device identity → authenticated communication → authorized services → role-controlled UI**

---

 # 13\. Resilience Architecture

 Define how SSP behaves when parts of the system become unavailable.

 ### 13.1 Edge unavailable

 ### 13.2 Cloud unavailable

 ### 13.3 Device communication interruption

 ### 13.4 Local buffering

 ### 13.5 Reconnection

 ### 13.6 Synchronization

 ### 13.7 Duplicate/conflicting data handling

 ### 13.8 Degraded operation

 ### 13.9 Recovery

 This section should demonstrate that resilience is an **architectural property**, not something added later.

---

 # 14\. Distributed Intelligence Architecture

 Keep this deliberately architectural.

 ### 14.1 Intelligence distribution

 ### 14.2 Device-level processing

 ### 14.3 Edge inference

 ### 14.4 Cloud analytics

 ### 14.5 Model/configuration path

 ### 14.6 Rationale for processing location

 The key D3 question is:

 > **Where should intelligence run, and why?**

 Detailed algorithms, datasets, training, accuracy and model-resource requirements belong to the later AI chapter/delivery.

---

 # 15\. Requirements-to-Architecture Traceability

 Demonstrate that D3 was derived from D2 rather than designed independently.

 Example:

 | D2 requirement | D3 architectural response |
| --- | --- |
| Local preprocessing | Device processing block |
| Local event detection | Device event-detection block |
| Adaptive sensing | Device sensing/energy management |
| ≥24 h buffering | Device/Edge buffering |
| Device–Edge latency requirement | C1 architecture |
| Edge processing | Edge processing subsystem |
| Low-latency inference | Edge inference block |
| Cloud scalability | Cloud service decomposition |
| Historical storage | Cloud storage subsystem |
| Privacy-aware processing | Local/Edge processing |
| Secure communication | Security functions at interfaces |
| Role-based access | Cloud identity/access subsystem |
| Configuration | Reverse communication path |
| Connectivity recovery | Buffering and synchronization |

The final table should contain the **actual frozen D2 requirements**, not placeholders.

---

 # 16\. Architectural Trade-offs and Design Decisions

 D3 should demonstrate engineering reasoning.

 ### 16.1 Device processing vs. energy consumption

 ### 16.2 Device processing vs. communication volume

 ### 16.3 Edge processing vs. edge computational requirements

 ### 16.4 Local buffering vs. memory requirements

 ### 16.5 Wireless range vs. energy consumption

 ### 16.6 Communication redundancy vs. complexity

 ### 16.7 Device AI vs. model complexity

 ### 16.8 Edge AI vs. latency

 ### 16.9 Cloud processing vs. connectivity dependence

 ### 16.10 Architecture vs. cost/scalability

 Each decision should ideally follow:

 > **Requirement → Alternatives → Constraint/trade-off → Architectural decision**

---

 # 17\. Final Selected SSP Architecture

 Only after the preceding analysis should D3 present the definitive architecture.

 The final diagram should show:

 - SSP Device(s);
- Edge/Mobile;
- Cloud;
- UI;
- principal functional blocks;
- C1/C2/C3 interfaces;
- major data flows;
- major control/configuration paths;
- security boundaries;
- buffering/resilience mechanisms;
- distributed intelligence locations.

 Conceptually:

```
                         SSP SYSTEM
                              │
       ┌──────────────────────┼──────────────────────┐
       │                      │                      │
       ▼                      ▼                      ▼
   DEVICE(S)                EDGE                   CLOUD
       │                      │                      │
 Sensors                 Gateway               Ingestion
 Processing              Validation             Storage
 Events                  Processing             Analytics
 Buffering               Local AI               AI/Models
 Energy                  Buffering               Management
 Security                Synchronization        Security
       │                      │                      │
       └─────── C1 ───────────┘                      │
                              │                      │
                              └──────── C2 ──────────┘
                                                     │
                                                     │ C3
                                                     ▼
                                                    UI
```

 The actual final diagram should be produced from the preceding analysis rather than assumed in advance.

---

 # 18\. Conclusion

 The conclusion should reinforce the project progression:

 > **SSP concept → use cases → D2 requirements → D3 architecture**

 It should state that:

 - the architecture was derived from the frozen D2 requirements;
- functions have been allocated across Device, Edge, Cloud and UI;
- communication interfaces have been defined;
- architectural security, resilience and distributed intelligence have been addressed;
- the selected architecture establishes the baseline for subsequent implementation/component selection.

 It should also explicitly establish the next boundary:

 > **D3 defines the logical architecture and communications architecture. Concrete hardware, software and platform selection are subsequent design activities.**

---

 # D3 Deliverables Checklist

 At the end of D3, we should have the following **frozen architectural artifacts**:

 ### A. Functional architecture

 **Function → Device / Edge / Cloud / UI**

 ### B. System block diagram

 **Device → Edge → Cloud → UI**

 ### C. Device block diagram

 Internal logical functions and interfaces.

 ### D. Edge block diagram

 Gateway + processing + buffering \+ inference + synchronization.

 ### E. Cloud block diagram

 Ingestion + processing + storage + analytics + management.

 ### F. UI architecture

 Monitoring + alerts + history \+ administration + control.

 ### G. Communications architecture

 **C1 + C2 + C3**

 ### H. Interface contracts

 Direction + purpose + data \+ performance + security \+ failure behavior.

 ### I. Principal data/control flows

 Normal operation + events \+ configuration + failure/recovery.

 ### J. Security architecture

 Identity + authentication \+ authorization + protected interfaces.

 ### K. Resilience architecture

 Buffering + degraded operation \+ recovery + synchronization.

 ### L. Distributed intelligence architecture

 Device vs. Edge vs. Cloud processing.

 ### M. D2 → D3 traceability matrix

 Requirements mapped to architectural mechanisms.

 ### N. Architectural decision/trade-off table

 Requirements mapped to design decisions.

 ### O. Final selected SSP architecture

 The **D3 architectural baseline** that subsequent deliveries must implement rather than redefine.

---

 ## Frozen D3 boundary

 The clean delivery boundary is therefore:

 **D2 — Requirements**

 > What must SSP do?

 ↓

 **D3 — Block & Communications Architecture**

 > Where are the functions performed, what are the logical blocks, and how do they communicate?

 ↓

 **D4 — Hardware / Platform / Implementation**

 > Which concrete components and technologies implement those blocks?

 ↓

 **D5 / AI**

 > How is the intelligence implemented and validated?

 ↓

 **Later chapters**

 > How are performance, economics, testing, scalability and final deployment demonstrated?

 This is the **updated D3 plan I recommend using as the working baseline going forward**.
