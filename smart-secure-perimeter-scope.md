 ## Frozen SSP Project Scope

 ### Project identity

 **SmartSecurePerimeter (SSP)** is an **IoT system-design and product-engineering project** for an intelligent, secure perimeter-monitoring platform based on a **Device–Edge–Cloud architecture**.

 The project will design a realistic, deployable solution assuming appropriate engineering resources. The laboratory implementation is a **separate Proof-of-Concept activity** and will not constrain the design of the real-world solution.

 ### Central design question

 > **How can an intelligent Device–Edge–Cloud IoT architecture improve the security, resilience, energy efficiency, privacy, and operational effectiveness of existing perimeter-monitoring solutions?**

 The project therefore focuses on **system engineering and integration**, rather than proposing a fundamentally new AI algorithm.

---

 ## Frozen system boundary

 The SSP system consists of three principal layers:

```
┌───────────────────────────────────────────────────────┐
│                       CLOUD                           │
│ Fleet intelligence │ Analytics │ Model management   │
│ Policies │ Historical data │ Dashboard │ APIs       │
└─────────────────────────▲─────────────────────────────┘
                          │
                    Internet / WAN
                          │
┌─────────────────────────┴─────────────────────────────┐
│                        EDGE                           │
│ Predictive geofencing │ Risk engine │ Privacy        │
│ Local AI │ Data reduction │ Connectivity fallback    │
└─────────────────────────▲─────────────────────────────┘
                          │
                    Local/Wireless
                          │
┌─────────────────────────┴─────────────────────────────┐
│                       DEVICE                          │
│ GNSS │ IMU │ Communications │ MCU/SoC │ AI          │
│ Power management │ Tamper detection │ Secure storage │
└───────────────────────────────────────────────────────┘
```

 ### Device

 The proposed intelligent monitoring device will address:

 - positioning;
- motion sensing;
- positioning confidence;
- local event detection;
- lightweight AI inference;
- adaptive energy management;
- tamper/security detection;
- secure communication.

 ### Edge

 The edge layer will address:

 - local decision-making;
- predictive geofencing;
- risk assessment;
- privacy-preserving data processing;
- communication optimization;
- operation during cloud/network disruption.

 ### Cloud

 The cloud layer will address:

 - fleet management;
- historical analytics;
- model management;
- policy management;
- cross-device intelligence;
- operational visualization;
- long-term storage and reporting.

---

 ## What is explicitly inside the scope

 The SSP design will investigate and specify:

 1. Existing perimeter-monitoring solutions and their documented characteristics.
2. Technical gaps that motivate the SSP architecture.
3. Functional and non-functional requirements.
4. Device hardware architecture and component selection.
5. Embedded software architecture.
6. Device-level intelligence.
7. Energy-management strategy.
8. Edge hardware/software architecture.
9. Predictive geofencing and risk intelligence.
10. Privacy-aware data processing.
11. Cloud architecture and data management.
12. Cloud AI/fleet intelligence.
13. End-to-end Device–Edge–Cloud data and decision flows.
14. Security and privacy architecture.
15. Quantifiable engineering KPIs.
16. Prototype/PoC implementation.
17. Testing and validation.
18. Deployment and scalability.
19. Economic and TCO analysis.
20. Limitations, risks and future development.

---

 ## What is explicitly _not_ the primary scope

 This is equally important.

 SSP is **not primarily**:

 - a new-AI-algorithm research thesis;
- a laboratory reverse-engineering exercise;
- a recreation of a commercial ankle monitor using whatever components happen to be available;
- a project whose final architecture is dictated by the laboratory equipment;
- merely an Android/BLE demonstration;
- merely a cloud dashboard;
- merely a GPS/geofencing application.

 AI is therefore treated as an **engineering capability within the architecture**, not as the sole research contribution.

---

 # Frozen 17-Chapter Structure

 We should now return to the structure you previously froze and use it as the **official report skeleton**:

 ### 1\. Problem / Use Case

 Problem definition, context, pain points, applications and proposed SSP concept.

 ### 2\. Target Users & Stakeholders

 Personas, stakeholders, responsibilities, needs and adoption environment.

 ### 3\. Requirements

 Functional, performance, security, privacy, energy, scalability and other measurable requirements.

 ### 4\. Market / Context Analysis

 Existing solutions, alternatives, competitors, documented capabilities, limitations, regulatory/contextual considerations and differentiation.

 ### 5\. IoT Architecture

 Overall Device–Edge–Cloud architecture, interfaces, communication paths and system responsibilities.

 ### 6\. Hardware

 Device architecture, sensors, MCU/SoC, communications, power, battery, security hardware and component selection.

 ### 7\. Communication

 BLE, cellular, Wi-Fi, GNSS-related communications, protocols, networking architecture and communication trade-offs.

 ### 8\. Software

 Embedded software, mobile/edge software, backend, APIs, application layer and software architecture.

 ### 9\. Data Flow

 Complete data lifecycle:

 > sensing → processing → decision → transmission → storage → analytics → visualization/action.

 ### 10\. AI / EdgeAI

 Device AI, Edge AI, cloud AI, model placement, inputs/outputs and rationale for where intelligence is executed.

 ### 11\. Energy / Performance

 Energy budget, latency, throughput, memory, computation, battery autonomy, duty cycle and performance constraints.

 ### 12\. Cloud Architecture

 Backend, database, APIs, authentication, storage, analytics, model management and operator interface.

 ### 13\. PoC

 The laboratory implementation demonstrating the **same system concept**, while clearly distinguishing what is simulated or substituted because of laboratory constraints.

 ### 14\. Business / Costs / Scalability

 BOM, development cost, operating cost, TCO, business model, manufacturing considerations and scaling from prototype to deployment.

 ### 15. Testing & Validation

 Test methodology, experiments, measurements, acceptance criteria, KPI verification and comparison against the defined baseline.

 ### 16\. Reports / Presentations / Defence

 Design documentation, diagrams, presentation material, demonstrations and defence preparation.

 ### 17\. Completeness / Critical Assessment

 Limitations, assumptions, risks, unresolved issues, lessons learned, improvements and future development.

---

 # How the detailed 24-chapter version fits later

 We should **not create a second competing structure**.

 Instead, the future 24-chapter version will be a **decomposition of these 17 chapters**.

 For example:

```
17-CHAPTER STRUCTURE
        │
        ├── 5. IoT Architecture
        │       ├── Overall architecture
        │       ├── Device architecture
        │       ├── Edge architecture
        │       └── Cloud architecture
        │
        ├── 6. Hardware
        │       ├── Device hardware
        │       ├── Component selection
        │       └── Power/security hardware
        │
        ├── 10. AI / EdgeAI
        │       ├── Device intelligence
        │       ├── Edge intelligence
        │       └── Cloud intelligence
        │
        └── 15. Testing & Validation
                ├── Device tests
                ├── Edge tests
                ├── Cloud tests
                └── End-to-end validation
```

 Thus, **17 chapters = frozen academic structure**, while **24 chapters = later detailed writing structure**.

 That avoids structural drift.

---

 # The baseline-to-SSP methodology is also frozen

 Every major technical section should follow the same engineering logic:

 > **Existing solution → limitation/gap → requirement → SSP design → design rationale → KPI → validation**

 For example:

```
Existing device
      ↓
High energy consumption
      ↓
Energy requirement
      ↓
Adaptive sensing architecture
      ↓
Hardware/software design
      ↓
Energy KPI
      ↓
Measured validation
```

 This gives the entire report a consistent engineering argument.

---

 # PoC boundary is frozen separately

 The **real-world SSP design** and the **laboratory PoC** must never be confused.

 ### Real-world design

 Assumes:

 - appropriate wearable hardware;
- appropriate GNSS;
- cellular connectivity;
- appropriate sensors;
- secure hardware;
- production-oriented power architecture;
- appropriate edge gateway;
- cloud infrastructure;
- adequate engineering resources.

 ### Laboratory PoC

 May use substitutions such as:

 > PCB + BLE + Android phone

 to emulate the functions of unavailable production hardware.

 The PoC therefore demonstrates:

 > **architecture and functionality**

 rather than claiming to be the final production device.

 This distinction should appear explicitly in Chapters 6, 13 and 17.

---

 ## Final scope statement

 I recommend that we now treat the following as the **frozen SSP scope statement**:

 > **SSP is an IoT system-design and product-engineering project that designs an intelligent Device–Edge–Cloud platform for secure perimeter monitoring. The project addresses identified limitations of existing monitoring architectures through an integrated combination of intelligent device sensing, adaptive energy management, positioning and motion intelligence, predictive edge processing, privacy-aware communication, cloud-based fleet intelligence, and scalable operational management. The proposed architecture is evaluated through measurable technical, energy, security, privacy, performance and economic KPIs. A laboratory PoC will demonstrate the architecture using available laboratory resources and may substitute or emulate production components where necessary; such substitutions do not redefine the real-world SSP design.**
