## Chapter 16 plan — Reports, Presentations and Defence

 Chapter 16 should **not introduce new technical design decisions**. Its purpose is to organize the engineering work from Chapters 1–15 into a coherent professional deliverable and prepare the evidence needed to defend the SSP design.

 The chapter will follow the frozen structure exactly:

 1. **16.1 Design report structure** — explain how the 17 chapters form one engineering argument.
2. **16.2 Executive summary** — define what the final executive summary must communicate.
3. **16.3 Technical diagrams** — establish the diagram set required to explain SSP clearly.
4. **16.4 Architecture diagrams** — define the principal system, deployment and security diagrams.
5. **16.5 Data-flow diagrams** — show the complete generated → processed → transmitted → stored → consumed chain.
6. **16.6 Tables and design decisions** — preserve traceability of requirements, alternatives and decisions.
7. **16.7 Partial defence** — structure the intermediate academic/technical presentation.
8. **16.8 Final defence** — structure the final presentation around problem, design, evidence and conclusions.
9. **16.9 PoC demonstration** — explain how the laboratory demonstration supports the design without redefining it.
10. **16.10 Presentation structure** — define the recommended presentation sequence.
11. **16.11 Anticipated defence questions** — identify the questions likely to challenge architectural decisions.
12. **16.12 Evidence supporting design decisions** — identify what evidence should be available for every major decision.

 The central principle will be:

 > **The report explains the design; the diagrams explain the system; the PoC demonstrates selected functionality; the validation evidence supports the claims; the defence explains and justifies the decisions.**

---

 # Chapter 16 — Reports / Presentations / Defence

 ## 16.1 Design Report Structure

 The SSP report should present the project as a coherent engineering development rather than as a collection of independent technical chapters.

 The logical progression established by the frozen project structure is:

 **Problem → Stakeholders → Requirements → Market/Context → Architecture → Hardware → Communication → Software → Data → AI → Energy/Performance → Cloud → PoC → Business/Scalability → Validation → Defence → Critical Assessment**

 Each chapter should therefore answer a specific engineering question.

 | Chapter | Engineering question |
| --- | --- |
| 1 | What problem are we solving? |
| 2 | Who needs and operates the solution? |
| 3 | What must the system achieve? |
| 4 | What already exists and what does the context imply? |
| 5 | How should the complete IoT system be organized? |
| 6 | What physical hardware is required? |
| 7 | How will the system communicate? |
| 8 | What software implements the system? |
| 9 | How does information move through the system? |
| 10 | Where and why is AI used? |
| 11 | Can the constrained device meet energy/performance requirements? |
| 12 | How is the cloud/backend implemented? |
| 13 | What part of the design can be demonstrated experimentally? |
| 14 | Can the proposed system be developed and scaled economically? |
| 15 | How will the design be tested and validated? |
| 16 | How is the complete engineering argument communicated and defended? |
| 17 | What remains uncertain, limited or unresolved? |

This structure prevents the later chapters from becoming disconnected from the original problem.

---

 ## 16.2 Executive Summary

 The executive summary should provide a concise description of the complete SSP proposal for a reader who may not read the full report.

 It should answer five questions:

 1. **What is SSP?**
2. **What problem does it address?**
3. **How is the system architected?**
4. **What are the principal engineering decisions?**
5. **How will the design be demonstrated and validated?**

 The executive summary should describe SSP as a complete real-world IoT system rather than as the laboratory prototype.

 A recommended structure is:

 **Problem → Proposed solution → Architecture → Key innovations/design characteristics → Validation approach → Expected contribution**

 The summary should avoid claiming measured performance before the corresponding validation work has been completed.

 For example, the report should distinguish between:

 > "The design targets an end-to-end alert latency of X seconds."

 and:

 > "The system achieved an end-to-end alert latency of X seconds."

 The first is a design requirement.

 The second is an experimental result.

 Only the latter should be stated after the relevant validation experiment has been performed.

---

 ## 16.3 Technical Diagrams

 SSP is sufficiently complex that diagrams are necessary for communicating the architecture efficiently.

 The final report should contain diagrams at several abstraction levels.

 ### Conceptual level

 A simplified representation should communicate:

 **Device → Edge/Mobile → Cloud → User**

 with feedback/control paths where relevant.

 ### Functional level

 The system should be represented through functions such as:

 **Sense → Interpret → Assess → Communicate → Store → Alert → Act**

 ### Technical level

 The technical architecture should identify representative components such as:

 - sensors;
- MCU/SoC;
- BLE;
- mobile/Edge application;
- cellular/WAN;
- API gateway;
- backend services;
- databases;
- AI services;
- dashboard;
- authentication;
- monitoring.

 ### Operational level

 The report should also show how a physical event becomes an operational response:

 **Physical event → sensing → local processing → Edge assessment → cloud processing → event → alert → operator action**

 These diagrams should use consistent terminology throughout the report.

---

 ## 16.4 Architecture Diagrams

 Several architecture diagrams should be maintained because one diagram cannot communicate every aspect of SSP adequately.

 ### 16.4.1 Overall architecture

 The principal diagram should show:

```
┌──────────────────────┐
│   SSP Device         │
│ Sensors / MCU / PMIC │
└──────────┬───────────┘
           │ BLE
           ▼
┌──────────────────────┐
│   Edge / Mobile      │
│ Fusion / Processing  │
└──────────┬───────────┘
           │ WAN
           ▼
┌──────────────────────┐
│       Cloud          │
│ APIs / Data / AI     │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ User / Operator      │
│ Dashboard / Alerts   │
└──────────────────────┘
```

 This is the principal architectural representation established in Chapter 5.

 ### 16.4.2 Deployment architecture

 The deployment diagram should distinguish:

 - wearable device;
- monitored person/environment;
- smartphone or Edge gateway;
- cellular/WAN infrastructure;
- Internet;
- cloud infrastructure;
- operator environment.

 ### 16.4.3 Security architecture

 A separate diagram should show security boundaries and trust relationships.

 For example:

 **Device trust boundary → Edge trust boundary → Cloud trust boundary → User trust boundary**

 The diagram should identify where authentication, authorization and encryption are applied.

 ### 16.4.4 Failure/recovery architecture

 Because resilience is one of SSP's design principles, the architecture documentation should also show important fallback paths.

 For example:

 **Normal path**

 Device → Edge → Cloud → User

 **Communication degradation**

 Device → Local processing → Store → Retry

 **Edge unavailable**

 Device → Local fallback → WAN/alternative path where supported

 The final diagrams should correspond to the actual architecture specified in Chapters 5–12.

---

 ## 16.5 Data-Flow Diagrams

 The data-flow diagrams should complement the architecture diagrams.

 The fundamental SSP data lifecycle is:

 **Generated → Acquired → Processed → Transmitted → Stored → Analyzed → Presented → Acted upon**

 The diagram should identify where each transformation occurs.

 | Stage | Principal location |
| --- | --- |
| Sensor generation | Device |
| Acquisition | Device |
| Initial filtering | Device |
| Sensor fusion | Device/Edge |
| Context interpretation | Edge |
| Event assessment | Edge/Cloud |
| Long-term storage | Cloud |
| Historical analysis | Cloud |
| AI model training | Cloud |
| Real-time presentation | User interface |
| Operational response | Authorized user/operator |

Data-flow diagrams should distinguish different data categories, for example:

 - raw sensor data;
- processed sensor data;
- position data;
- device-health data;
- event data;
- alert data;
- configuration data;
- AI-derived information;
- audit information.

 This distinction is important because SSP does not necessarily need to transmit all raw information continuously.

---

 ## 16.6 Tables and Design Decisions

 A professional engineering report should make important decisions traceable.

 The principal design decisions should therefore be documented in structured tables.

 ### Requirements traceability

 **Requirement → Architecture → Component → Test**

 ### Technology selection

 **Alternative → Criteria → Evaluation → Decision → Rationale**

 ### Architecture decisions

 **Decision → Motivation → Consequence → Validation method**

 ### Risk decisions

 **Risk → Mitigation → Residual risk → Validation**

 A recommended design-decision record is:

 | Field | Description |
| --- | --- |
| Decision ID | Unique identifier |
| Decision | What was selected? |
| Alternatives | What alternatives were considered? |
| Drivers | Which requirements influenced the decision? |
| Rationale | Why was the decision made? |
| Consequences | What does the decision enable or constrain? |
| Validation | How will the decision be tested? |
| Status | Proposed / frozen / validated |

This is especially valuable because SSP has deliberately separated:

 **requirements → architecture → implementation → validation**

 The report should preserve that separation.

---

 ## 16.7 Partial Defence

 The partial defence should demonstrate that the project has progressed from a problem statement to a coherent engineering design.

 The presentation should therefore focus on the design reasoning rather than attempting to present every technical detail.

 A suitable sequence is:

 1. Problem and motivation
2. Target users and operational scenario
3. Requirements
4. Market/context findings
5. SSP architecture
6. Hardware concept
7. Communication architecture
8. Software/data architecture
9. AI strategy
10. Energy/performance considerations
11. Cloud architecture
12. PoC strategy
13. Remaining engineering work

 The partial defence should demonstrate that:

 > **The architecture is a consequence of the requirements and context analysis.**

 This is more important than simply showing a large number of technical components.

---

 ## 16.8 Final Defence

 The final defence should present SSP as a completed engineering design with supporting evidence.

 A recommended structure is:

 ### Part I — Problem

 - problem statement;
- operational context;
- users;
- use cases.

 ### Part II — Engineering requirements

 - functional requirements;
- performance requirements;
- security/privacy;
- energy;
- reliability.

 ### Part III — Design

 - overall architecture;
- hardware;
- communication;
- software;
- data flow;
- AI;
- cloud.

 ### Part IV — Demonstration

 - PoC architecture;
- demonstration scenario;
- observed functionality.

 ### Part V — Validation

 - test methodology;
- key measurements;
- requirement traceability;
- identified failures and corrections.

 ### Part VI — Business and deployment

 - cost structure;
- scalability;
- deployment strategy.

 ### Part VII — Critical assessment

 - limitations;
- risks;
- unresolved engineering questions;
- future work.

 The defence should therefore follow the same logical sequence as the report.

---

 ## 16.9 PoC Demonstration

 The PoC demonstration should explicitly preserve the distinction between the real-world SSP design and the laboratory implementation.

 The presentation should begin by stating:

 > **The laboratory PoC demonstrates selected SSP functions; it is not the complete production implementation of the SSP system.**

 A representative demonstration sequence could be:

 1. Start the laboratory device.
2. Acquire sensor information.
3. Establish BLE communication.
4. Transfer information to the mobile/Edge application.
5. Process the incoming data.
6. Generate a representative event.
7. Send structured information to the backend.
8. Store the event.
9. Display the event on the frontend.
10. Demonstrate a communication interruption.
11. Demonstrate recovery where implemented.

 The demonstration should be short enough to be reliable but comprehensive enough to prove the complete IoT chain.

 The PoC should specifically demonstrate the course-relevant chain:

 **MCU → BLE → Android/Edge → JSON/API → Cloud → Frontend**

 where these functions correspond to the laboratory implementation.

---

 ## 16.10 Presentation Structure

 The final presentation should avoid reproducing the entire report.

 Instead, the presentation should answer:

 **Why this problem?**

 ↓

 **What does SSP need to achieve?**

 ↓

 **Why this architecture?**

 ↓

 **Why these technologies?**

 ↓

 **How does information flow?**

 ↓

 **Where is AI useful?**

 ↓

 **Can the system meet the requirements?**

 ↓

 **What was demonstrated?**

 ↓

 **What remains unresolved?**

 A practical presentation structure is therefore:

 | Section | Approximate emphasis |
| --- | --- |
| Problem/use case | Short |
| Requirements | Short–medium |
| Market/context | Short |
| Architecture | High |
| Hardware/communication/software | High |
| AI | Medium |
| Energy/performance | Medium |
| Cloud/data | Medium |
| PoC | High |
| Validation | High |
| Business/scalability | Medium |
| Limitations/future work | Medium |

The exact duration will depend on the course's presentation constraints.

---

 ## 16.11 Anticipated Defence Questions

 The defence should be prepared around questions that challenge the engineering rationale rather than merely requesting definitions.

 ### Problem and requirements

 **Why is IoT appropriate for this problem?**

 The answer should connect physical-world sensing, connectivity and operational response.

 **Which requirement is most difficult to satisfy?**

 The answer should identify the relevant technical constraint and explain how it is being addressed.

 **Which requirements are measurable?**

 The answer should refer directly to Chapter 3.

---

 ### Architecture

 **Why is processing distributed instead of performed entirely in the cloud?**

 The answer should discuss latency, energy, resilience, privacy and connectivity.

 **Why is an Edge/Mobile layer required?**

 The answer should identify functions for which local processing provides a measurable benefit.

 **What happens if the cloud is unavailable?**

 The answer should refer to the fallback architecture.

---

 ### Hardware

 **Why was this MCU/SoC selected?**

 The answer should connect computational capability, interfaces, energy, memory and connectivity requirements.

 **Why were these sensors selected?**

 The answer should connect sensor characteristics to the required measurements.

 **What is the most significant hardware constraint?**

 The answer should be supported by Chapter 11's energy/performance analysis.

---

 ### Communication

 **Why was this communication technology selected?**

 The answer should compare:

 - range;
- bandwidth;
- latency;
- energy;
- infrastructure;
- cost;
- reliability.

 **What happens when communication fails?**

 The answer should explain the fallback behavior.

---

 ### AI

 **Why do we need AI?**

 The answer should identify the specific problem that AI addresses.

 **Could a deterministic algorithm solve the same problem?**

 The answer should acknowledge this possibility and explain the proposed benchmark.

 **Where should AI run?**

 The answer should be based on latency, computational resources, privacy, energy and data requirements.

---

 ### Energy

 **How long should the battery last?**

 The answer should refer to the Chapter 11 energy model and subsequently to Chapter 15 validation.

 **Which function consumes the most energy?**

 The answer should be based on measured or analytically estimated consumption rather than assumption.

---

 ### Security and privacy

 **How is the device authenticated?**

 **How are communications protected?**

 **What happens if a device is stolen?**

 **What information is retained in the cloud?**

 These questions should be answered using the security and privacy architecture developed throughout Chapters 5–12.

---

 ### Validation

 **How do you know the system works?**

 The answer should follow:

 **Requirement → Metric → Test → Result**

 **What happens if a requirement fails?**

 The answer should describe the failure-analysis and redesign loop.

---

 ### PoC

 **Why doesn't the laboratory hardware match the proposed production hardware?**

 The answer should explicitly refer to the frozen project principle:

 > The PoC demonstrates the IoT concept using available laboratory resources; it does not redefine the real-world product architecture.

---

 ## 16.12 Evidence Supporting Design Decisions

 Every significant engineering decision should have evidence behind it.

 Evidence can originate from several sources:

 - Chapter 3 requirements;
- Chapter 4 market/context analysis;
- technical datasheets;
- standards;
- engineering calculations;
- technology comparisons;
- simulations;
- laboratory measurements;
- PoC results;
- validation experiments;
- cost estimates;
- security analysis.

 The evidence hierarchy should distinguish between:

 ### Documented evidence

 For example:

 > A component datasheet specifies a particular current consumption.

 ### Analytical evidence

 For example:

 > An energy model predicts a particular battery-life range.

 ### Experimental evidence

 For example:

 > Laboratory measurements show the measured current under a defined operating condition.

 ### Product-level evidence

 For example:

 > Environmental testing confirms operation across the specified temperature range.

 These should not be treated as equivalent.

 The report should clearly state which type of evidence supports each conclusion.

---

 ## 16.13 Engineering Decision Traceability

 The complete SSP project should ultimately be traceable through the following chain:

 **Chapter 1**

 Problem

 ↓

 **Chapter 2**

 Stakeholder needs

 ↓

 **Chapter 3**

 Requirements

 ↓

 **Chapter 4**

 Market/context evidence

 ↓

 **Chapter 5**

 Architecture decisions

 ↓

 **Chapters 6–12**

 Technical implementation decisions

 ↓

 **Chapter 13**

 PoC demonstration

 ↓

 **Chapter 14**

 Business/scalability assessment

 ↓

 **Chapter 15**

 Validation

 ↓

 **Chapter 16**

 Communication and defence

 ↓

 **Chapter 17**

 Critical assessment

 This traceability is important because it prevents a common weakness in engineering reports: introducing technologies first and only later attempting to justify why they were required.

 SSP should instead demonstrate:

 > **The requirements created the design constraints; the design constraints guided the technology choices; the technology choices created measurable consequences; and validation determines whether those consequences satisfy the requirements.**

---

 ## 16.14 Final Documentation Checklist

 Before the final submission, the SSP documentation should be checked for consistency.

 ### Technical consistency

 - [ ] Architecture diagrams match the written architecture.
- [ ] Hardware described in Chapter 6 matches the architecture.
- [ ] Communication technologies match Chapter 7.
- [ ] Software components match Chapter 8.
- [ ] Data flows match Chapter 9.
- [ ] AI functions match Chapter 10.
- [ ] Energy assumptions match Chapter 11.
- [ ] Cloud components match Chapter 12.
- [ ] PoC architecture matches Chapter 13.
- [ ] Validation tests correspond to Chapter 15.

 ### Requirements consistency

 - [ ] Important requirements have measurable criteria.
- [ ] Major design decisions trace back to requirements.
- [ ] Validation tests trace back to requirements.
- [ ] Claimed performance is distinguished from target performance.

 ### Evidence consistency

 - [ ] Technical claims have appropriate sources.
- [ ] Component specifications use manufacturer documentation where applicable.
- [ ] Calculated values identify their assumptions.
- [ ] Experimental values identify the test conditions.
- [ ] Unverified assumptions are clearly labelled.

 ### Presentation consistency

 - [ ] Report terminology is consistent.
- [ ] Diagram terminology is consistent.
- [ ] PoC terminology is consistent.
- [ ] Presentation claims match the report.
- [ ] No unmeasured result is presented as an achieved result.

---

 ## 16.15 Chapter 16 Conclusion

 Chapter 16 establishes how the SSP engineering work will be communicated, demonstrated and defended.

 The report should be presented as a continuous engineering argument:

 **Problem → Requirements → Evidence → Architecture → Implementation → Validation → Assessment**

 The diagrams should provide multiple views of the same system:

 **Architecture view → Deployment view → Data-flow view → Security view → Operational view**

 The PoC should demonstrate the essential IoT chain without being mistaken for the complete production system.

 The final defence should focus on **engineering reasoning** rather than simply presenting a catalogue of technologies. The central question is not:

 > "Which technologies did SSP use?"

 but:

 > **"Why were these technologies and architectural decisions selected, what requirements do they satisfy, and what evidence supports the resulting design?"**

 Finally, Chapter 16 establishes an important principle for the final report:

 > **Every significant SSP claim should be traceable either to a requirement, a documented source, an engineering calculation, or experimental evidence.**

 This prepares the project for the final chapter, where the complete design will be critically assessed rather than simply presented as if all engineering uncertainties have already been resolved.
