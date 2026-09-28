# Chapter 16 — Reports, Presentations & Defence

 ## 16.1 Design Report Structure

 The SSP report should be presented as a **single engineering argument**, not as a collection of independent technical chapters.

 The complete progression is:

 **Problem → Stakeholders → Requirements → Context → Architecture → Hardware → Communication → Software → Data → AI → Energy/Performance → Cloud → PoC → Business/Scalability → Validation → Defence → Critical Assessment**

 | Chapter | Engineering question |
| --- | --- |
| 1 | What problem is SSP solving? |
| 2 | Who needs, operates and is affected by the system? |
| 3 | What must SSP achieve? |
| 4 | What does the existing context and technology landscape imply? |
| 5 | How should the complete IoT system be organized? |
| 6 | What physical hardware is required? |
| 7 | How will the system communicate? |
| 8 | What software implements the system? |
| 9 | How does information move through the system? |
| 10 | Where and why should AI be used? |
| 11 | Can the constrained device satisfy energy/performance requirements? |
| 12 | How should the cloud/backend operate? |
| 13 | What parts of the design can be demonstrated experimentally? |
| 14 | Can SSP be developed, operated and scaled economically? |
| 15 | How will the design be tested and validated? |
| 16 | How should the engineering argument be communicated and defended? |
| 17 | What remains uncertain, limited or unresolved? |

This progression prevents later chapters from becoming disconnected from the original problem.

---

 ## 16.2 Executive Summary

 The executive summary should allow a reader to understand the complete SSP proposal without reading the entire report.

 It should answer five questions:

 1. **What is SSP?**
2. **What problem does it address?**
3. **How is it architected?**
4. **What are its principal engineering decisions?**
5. **How will those decisions be demonstrated and validated?**

 A useful structure is:

 **Problem → Proposed solution → Architecture → Key design characteristics → Validation approach → Expected contribution**

 The summary must distinguish carefully between **targets** and **measured results**.

 For example:

 > "The design targets an end-to-end alert latency of X seconds."

 is a specification.

 Whereas:

 > "The system achieved an end-to-end alert latency of X seconds."

 is an experimental claim.

 The second statement should only appear after the corresponding test has actually been performed and documented.

 The executive summary should also identify SSP as the **complete intended IoT system**, rather than describing the laboratory PoC as though it were already the final production device.

---

 ## 16.3 Technical Diagrams

 SSP contains enough interacting subsystems that diagrams are essential for communicating the design efficiently.

 The final report should use several abstraction levels.

 ### Conceptual level

 The simplest representation should communicate:

 **Device → Edge/Mobile → Cloud → User**

 with relevant control or feedback paths.

 ### Functional level

 The functional chain can be represented as:

 **Sense → Interpret → Assess → Communicate → Store → Alert → Act**

 ### Technical level

 The technical diagram should identify representative elements such as:

 - sensors;
- MCU/SoC;
- BLE;
- mobile/Edge application;
- cellular/WAN;
- API gateway;
- backend services;
- databases;
- AI services;
- dashboards;
- authentication;
- monitoring.

 ### Operational level

 The physical-to-operational transformation should be visible:

 **Physical event → Sensing → Local processing → Edge assessment → Cloud processing → Event → Alert → Operator action**

 All diagrams should use the same terminology as the corresponding chapters.

---

 ## 16.4 Architecture Diagrams

 No single diagram can adequately communicate every aspect of SSP. The final documentation should therefore maintain several complementary architecture views.

 ### 16.4.1 Overall architecture

 The principal architecture diagram should be:

```
┌──────────────────────────┐
│       SSP Device         │
│ Sensors / MCU / Power    │
└────────────┬─────────────┘
             │ BLE
             ▼
┌──────────────────────────┐
│      Edge / Mobile       │
│ Fusion / Local Processing│
└────────────┬─────────────┘
             │ WAN
             ▼
┌──────────────────────────┐
│          Cloud           │
│ APIs / Data / AI / Mgmt  │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│     User / Operator      │
│ Dashboard / Alerts       │
└──────────────────────────┘
```

 This remains the primary representation of the architecture established in Chapter 5.

 ### 16.4.2 Deployment architecture

 The deployment view should distinguish:

 - wearable device;
- monitored person/environment;
- smartphone or Edge gateway;
- cellular/WAN infrastructure;
- Internet;
- cloud infrastructure;
- operator environment.

 This diagram should make physical deployment relationships clear.

 ### 16.4.3 Security architecture

 A dedicated security diagram should show:

 **Device trust boundary → Edge trust boundary → Cloud trust boundary → User trust boundary**

 It should identify the principal locations of:

 - authentication;
- authorization;
- encryption;
- credential management;
- secure storage;
- audit logging.

 ### 16.4.4 Failure/recovery architecture

 Because resilience is an explicit SSP design principle, fallback paths should also be documented.

 **Normal path**

```
Device → Edge → Cloud → User
```

 **Communication degradation**

```
Device → Local Processing → Local Storage → Retry → Synchronization
```

 **Edge unavailable**

```
Device → Local Fallback → Alternative/Deferred Communication
```

 Only fallback mechanisms actually supported by the final implementation should be shown as implemented capabilities.

---

 ## 16.5 Data-Flow Diagrams

 Architecture diagrams show **where** system components exist. Data-flow diagrams should show **how information moves and changes**.

 The fundamental SSP data lifecycle is:

 **Generated → Acquired → Processed → Transmitted → Stored → Analyzed → Presented → Acted Upon**

 | Stage | Principal location |
| --- | --- |
| Sensor generation | Device |
| Sensor acquisition | Device |
| Initial filtering | Device |
| Sensor fusion | Device/Edge |
| Context interpretation | Edge |
| Event assessment | Edge/Cloud |
| Long-term storage | Cloud |
| Historical analysis | Cloud |
| AI model development/training | Cloud/development environment |
| Real-time presentation | User interface |
| Operational response | Authorized operator |

The diagrams should distinguish between:

 - raw sensor data;
- processed sensor data;
- position information;
- device-health information;
- event information;
- alerts;
- configuration data;
- AI-derived information;
- audit information.

 This distinction is particularly important because SSP does not necessarily need to transmit every raw sensor measurement continuously.

 A well-designed data-flow diagram should therefore make clear **what is generated, what is retained, what is transmitted and what is discarded or transformed**.

---

 ## 16.6 Tables and Design Decisions

 A professional engineering report should preserve the reasoning behind major decisions.

 The principal traceability structures should include:

 ### Requirements

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
| Validation | How will it be tested? |
| Status | Proposed / Frozen / Validated |

This structure preserves the separation between:

 **Requirements → Architecture → Implementation → Validation**

 and makes later revisions much easier to manage.

---

 ## 16.7 Partial Defence

 The partial defence should demonstrate that the project has progressed from a problem statement to a coherent engineering design.

 It should focus on **engineering reasoning**, rather than attempting to present every implementation detail.

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

 The key message should be:

 > **The architecture is a consequence of the requirements and operating context.**

 The presentation should therefore show the chain of reasoning rather than simply display a list of technologies.

---

 ## 16.8 Final Defence

 The final defence should present SSP as an engineering design supported by appropriate evidence.

 A recommended structure is:

 ### Part I — Problem

 - problem statement;
- operational context;
- users;
- use cases.

 ### Part II — Requirements

 - functional requirements;
- performance requirements;
- security/privacy requirements;
- energy requirements;
- reliability requirements.

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
- observed functionality;
- known PoC limitations.

 ### Part V — Validation

 - test methodology;
- measurements;
- requirement traceability;
- failures;
- corrective actions.

 ### Part VI — Business and Deployment

 - cost structure;
- TCO;
- scalability;
- deployment strategy.

 ### Part VII — Critical Assessment

 - limitations;
- risks;
- unresolved engineering questions;
- future development.

 The defence should therefore follow the same fundamental logic as the report:

 **Problem → Requirements → Design → Evidence → Assessment**

---

 ## 16.9 PoC Demonstration

 The PoC demonstration must preserve the distinction between the **intended SSP product** and the **laboratory implementation**.

 The presentation should explicitly establish:

 > **The laboratory PoC demonstrates selected SSP functions; it is not the complete production implementation of the SSP system.**

 A representative demonstration sequence is:

 1. Start the laboratory device.
2. Acquire sensor information.
3. Establish BLE communication.
4. Transfer information to the mobile/Edge application.
5. Process the incoming information.
6. Generate a representative event.
7. Send structured information to the backend.
8. Store the event.
9. Display the event on the frontend.
10. Interrupt communication where the PoC supports this test.
11. Demonstrate recovery or deferred synchronization where implemented.

 The central demonstration chain is:

 **MCU → BLE → Android/Edge → JSON/API → Cloud → Frontend**

 The demonstration should be deliberately controlled. Reliability is more important than demonstrating a large number of features simultaneously.

 Any functionality not actually implemented should be identified as **planned, simulated or represented**, rather than presented as operational.

---

 ## 16.10 Presentation Structure

 The final presentation should not reproduce the report chapter by chapter.

 Instead, it should answer the central engineering questions:

 **Why this problem?**

 ↓

 **What must SSP achieve?**

 ↓

 **Why this architecture?**

 ↓

 **Why these technologies?**

 ↓

 **How does information flow?**

 ↓

 **Where is AI useful?**

 ↓

 **Can the system meet its requirements?**

 ↓

 **What has actually been demonstrated?**

 ↓

 **What remains unresolved?**

 A practical emphasis structure is:

 | Section | Suggested emphasis |
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

The exact timing should be adjusted to the course's presentation requirements.

---

 ## 16.11 Anticipated Defence Questions

 The strongest preparation is to anticipate questions that challenge the **engineering rationale**.

 ### Problem and requirements

 **Why is IoT appropriate for this problem?**

 The answer should connect physical-world sensing, connectivity, processing and operational response.

 **Which requirement is most difficult to satisfy?**

 The answer should identify the relevant constraint and explain how the architecture addresses it.

 **Which requirements are measurable?**

 The answer should refer directly to Chapter 3 and Chapter 15.

---

 ### Architecture

 **Why is processing distributed instead of performed entirely in the cloud?**

 The answer should address the relevant trade-offs involving latency, energy, resilience, privacy and connectivity.

 **Why is an Edge/Mobile layer required?**

 The answer should identify functions where local processing provides a measurable benefit.

 **What happens if the cloud becomes unavailable?**

 The answer should describe the defined fallback behavior and its limitations.

---

 ### Hardware

 **Why was this MCU/SoC selected?**

 The answer should connect:

 - processing capability;
- interfaces;
- memory;
- connectivity;
- power consumption;
- software requirements.

 **Why were these sensors selected?**

 The answer should connect sensor characteristics to the measurements required by Chapter 3.

 **What is the most significant hardware constraint?**

 The answer should be supported by the energy/performance analysis from Chapter 11.

---

 ### Communication

 **Why was this communication technology selected?**

 The answer should compare relevant factors such as:

 - range;
- bandwidth;
- latency;
- energy;
- infrastructure;
- cost;
- reliability.

 **What happens when communication fails?**

 The answer should describe the fallback and recovery mechanisms.

---

 ### AI

 **Why is AI needed?**

 The answer should identify the specific problem for which AI is being considered.

 **Could a deterministic algorithm solve the same problem?**

 The answer should acknowledge that possibility and explain the proposed AI-versus-baseline benchmark.

 **Where should AI run?**

 The answer should be based on:

 - latency;
- computation;
- privacy;
- energy;
- data availability.

---

 ### Energy

 **How long should the battery last?**

 The answer should refer to the Chapter 11 analytical model and subsequently to Chapter 15 measurements.

 **Which function consumes the most energy?**

 The answer should distinguish between an analytical estimate and a measured result.

---

 ### Security and privacy

 Potential questions include:

 **How is the device authenticated?**

 **How are communications protected?**

 **What happens if a device is stolen?**

 **What information is retained in the cloud?**

 **How are administrative privileges controlled?**

 The answers should reference the security and privacy architecture developed across Chapters 5–12.

---

 ### Validation

 **How do you know the system works?**

 The answer should follow:

 **Requirement → Metric → Test → Evidence → Result**

 **What happens if a requirement fails?**

 The answer should describe:

 **Measure → Analyze → Correct → Retest**

 rather than simply declaring the system unsuccessful or successful.

---

 ### PoC

 **Why doesn't the laboratory hardware match the proposed production hardware?**

 The answer should explicitly state:

 > **The PoC demonstrates the IoT concept using available laboratory resources; it does not redefine the real-world product architecture.**

 **Which parts of the final system are actually demonstrated?**

 The answer should identify the implemented functions precisely and separate them from planned production capabilities.

---

 ## 16.12 Evidence Supporting Design Decisions

 Every significant engineering decision should have identifiable supporting evidence.

 Possible evidence sources include:

 - Chapter 3 requirements;
- Chapter 4 market/context analysis;
- manufacturer datasheets;
- applicable standards;
- engineering calculations;
- technology comparisons;
- simulations;
- laboratory measurements;
- PoC results;
- Chapter 15 validation experiments;
- cost estimates;
- security analysis.

 Evidence should be categorized according to its strength and origin.

 ### Documented evidence

 Example:

 > A manufacturer datasheet specifies the component's stated current consumption under a defined operating condition.

 ### Analytical evidence

 Example:

 > An energy model predicts a battery-life range under defined assumptions.

 ### Experimental evidence

 Example:

 > Laboratory measurements record actual current consumption under a defined operating condition.

 ### Product-level evidence

 Example:

 > Environmental testing demonstrates operation across the specified temperature range.

 These forms of evidence should not be treated as interchangeable.

 A useful evidence statement therefore includes:

 **Claim → Evidence type → Source/measurement → Conditions → Limitation**

 This makes it much harder for an engineering estimate to accidentally become presented as an established fact.

---

 ## 16.13 Engineering Decision Traceability

 The complete SSP project should ultimately be traceable through:

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

 The central engineering argument is:

 > **The requirements created the design constraints; the constraints guided the technology choices; the technology choices created measurable consequences; and validation determines whether those consequences satisfy the requirements.**

 This traceability prevents a common weakness in engineering projects: selecting technologies first and attempting to justify them afterwards.

---

 ## 16.14 Final Documentation Checklist

 Before submission, the entire SSP documentation should be checked for consistency.

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
- [ ] Chapter 16 presentation material does not introduce undocumented architecture.

 ### Requirements consistency

 - [ ] Important requirements have measurable criteria.
- [ ] Major design decisions trace back to requirements.
- [ ] Validation tests trace back to requirements.
- [ ] Target performance is distinguished from demonstrated performance.
- [ ] Unsupported claims have been removed or clearly labelled as assumptions.

 ### Evidence consistency

 - [ ] Technical claims have appropriate sources.
- [ ] Component specifications use manufacturer documentation where applicable.
- [ ] Calculated values identify their assumptions.
- [ ] Experimental values identify test conditions.
- [ ] PoC observations are distinguished from product-level validation.
- [ ] Unverified assumptions are clearly labelled.

 ### Presentation consistency

 - [ ] Report terminology is consistent.
- [ ] Diagram terminology is consistent.
- [ ] PoC terminology is consistent.
- [ ] Presentation claims match the report.
- [ ] No unmeasured result is presented as an achieved result.
- [ ] Slides do not imply product certification or production readiness without evidence.
- [ ] The final presentation distinguishes requirements, estimates, demonstrations and validated results.

---

 ## 16.15 Chapter 16 Conclusion

 Chapter 16 establishes how the SSP engineering work is communicated, demonstrated and defended.

 The complete report should form a continuous engineering argument:

 **Problem → Requirements → Evidence → Architecture → Implementation → Validation → Assessment**

 The diagrams should provide complementary views of the same system:

 **Architecture → Deployment → Data Flow → Security → Operations**

 The PoC should demonstrate the essential IoT chain without being mistaken for the complete production system.

 The final defence should concentrate on **engineering reasoning** rather than presenting a catalogue of technologies. The central question is not simply:

 > "Which technologies did SSP use?"

 but:

 > **"Why were these technologies and architectural decisions selected, which requirements do they address, what consequences do they introduce, and what evidence supports the resulting design?"**

 Every significant SSP claim should therefore be traceable to at least one of four evidence categories:

 **Requirement → Documented Source → Engineering Calculation → Experimental Evidence**

 The chapter also establishes an important discipline for the final submission: **the confidence of a conclusion must match the evidence available for it**.

 A requirement is not a result.

 A calculation is not a measurement.

 A PoC demonstration is not automatically product validation.

 A technical possibility is not automatically a production capability.

 A planned feature is not an implemented feature.

 Maintaining these distinctions substantially strengthens the credibility of the engineering report and the final defence.

 The resulting documentation chain is:

 **Requirements → Design → Implementation → Demonstration → Measurement → Validation → Communication → Critical Assessment**

 This prepares SSP for the final chapter, where the complete project can be examined critically, including its technical limitations, assumptions, unresolved questions, risks and opportunities for future development.
