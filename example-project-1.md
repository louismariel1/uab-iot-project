 ## TD1 — Derived structure of Project 1

 From the material provided, P1 follows this overall structure:

 1. **Introduction / problem definition**
   - Environmental acoustic monitoring as the central problem.
   - Motivation for continuous, distributed monitoring.
   - Limitations of conventional/manual noise monitoring.
2. **System objectives and requirements**
   - Functional requirements.
   - Non-functional/performance requirements.
   - Acoustic measurement requirements.
   - Communication, energy, latency, reliability and classification targets.
3. **System architecture**
   - Four-layer IoT architecture:\
      **Device → Communication/Edge → Cloud → User interface**.
   - Definition of the node, gateway, cloud backend and dashboards.
4. **Hardware design**
   - MEMS microphone.
   - MCU/SoC.
   - LoRa/sub-GHz communication.
   - Power-management circuitry.
   - Battery and solar harvesting for outdoor nodes.
   - Indoor/outdoor enclosure design.
   - Gateway hardware.
5. **Embedded/device software**
   - Acoustic acquisition.
   - Feature extraction.
   - Local inference.
   - Data packaging.
   - Power management.
   - Wireless transmission.
6. **Communication subsystem**
   - LoRa/LPWAN-based campus communication.
   - Gateway topology.
   - Range and packet-delivery targets.
   - Gateway capacity and channel occupancy.
   - Local buffering and packet-loss estimation.
7. **AI / TinyML**
   - Acoustic-event classification.
   - On-device inference.
   - Macro-F1 target.
   - Confidence threshold and `unknown` class.
   - Temporal smoothing/majority voting.
8. **Cloud and user interface**
   - Data ingestion.
   - Processing and alerting.
   - Database/storage.
   - APIs/backend.
   - Web/mobile dashboards.
   - Multi-tenant architecture.
   - Availability and query-performance targets.
9. **Energy and performance analysis**
   - Device current consumption.
   - Duty cycles.
   - Average power.
   - Battery autonomy.
   - Solar sizing.
   - Winter energy margin.
   - Environmental operating conditions.
10. **Implementation / PoC / validation**
    - Hardware/software implementation choices.
    - Prototype validation.
    - Performance KPI analysis.
    - Testing and certification planning.
    - Transition toward a 500-node deployment.
11. **Deployment and scalability**
    - 10-node pilot.
    - 500-node campus deployment.
    - Gateway sizing.
    - Manufacturing considerations.
    - Industrialization roadmap.
12. **Economic and business analysis**
    - NRE.
    - Personnel.
    - Indirect costs.
    - TCO.
    - Pricing.
    - Business model.
    - Commercialization roadmap.
    - Break-even analysis.
13. **Project planning**
    - 24-month GANTT.
    - Milestones.
    - Manufacturing readiness.
    - Commercial launch.
14. **Conclusion**
    - Technical feasibility.
    - Economic feasibility.
    - Scalability.
    - Commercial readiness.
15. **Team roles and AI-tool disclosure**
16. **References**
17. **Appendices**
    - KPI summary.
    - Power-consumption calculations.
    - Component-selection alternatives.
    - Full GANTT.

 So, structurally, P1 is not merely a hardware prototype report. It is organized as an **end-to-end IoT product-development project**, progressing from problem → requirements → architecture → implementation → validation → economics → commercialization.

---

 # TD2 — Mapping P1 against the derived template

 | Template element | Where/how P1 addresses it | Assessment |
| --- | --- | --- |
| **Problem / use case** | Environmental acoustic monitoring; continuous monitoring of campus/municipal noise conditions. | **Strong** |
| **Target users and stakeholders** | Universities, municipalities, campus operators and customers; operational/support stakeholders are also implicit. | **Good**, but stakeholder roles could be made more explicit. |
| **Requirements** | System KPIs, acoustic accuracy, latency, PDR, energy, storage, availability, classifier Macro-F1, gateway capacity, etc. | **Very strong** |
| **Market/context analysis** | Discussion of environmental monitoring, existing solutions, target B2B customers and commercialization. | **Present**, but could use more explicit competitor/market evidence. |
| **IoT architecture** | Device → gateway/communication → cloud → web/mobile UI. | **Very strong** |
| **Hardware** | MEMS microphone, ESP32-S3/MCU alternatives, LoRa radio, PMIC, battery, solar panel, enclosure, gateway. | **Very strong** |
| **Communication** | LoRa/LPWAN, gateway topology, range, PDR, channel occupancy, packet-loss definition. | **Very strong** |
| **Software** | Embedded processing, TinyML, backend, database, dashboards, web/mobile interfaces. | **Strong** |
| **Data flow** | Acoustic signal → feature extraction/classification → compact payload → LoRa → gateway → cloud → database/dashboard. | **Strong**, although a dedicated data-flow diagram would improve clarity. |
| **AI / EdgeAI** | TinyML acoustic classifier, 1-s decision window, majority voting, Macro-F1 ≥ 0.85, confidence threshold. | **Very strong** |
| **Energy/performance** | Detailed current/duty-cycle table, 10.8 mW calculation, battery autonomy, solar sizing and winter margin. | **Very strong** |
| **Cloud architecture** | Ingestion, processing/alerts, database, storage, queries, availability, multi-tenancy. | **Strong** |
| **PoC** | Pilot deployment of 10 nodes; implementation and validation of system components. | **Present**, but the distinction between _implemented prototype_ and _planned commercial system_ should be clearer. |
| **Business model, costs and scalability** | NRE, TCO, pricing, 500-node deployment, subscriptions, commercialization, break-even. | **Exceptionally comprehensive** |
| **Testing and validation** | KPI targets, acoustic accuracy, PDR, energy calculations, classification targets, certification planning. | **Good**, but some results appear to be estimates/targets rather than experimentally demonstrated results. |
| **Reports/presentations/defence** | GANTT, team roles, AI-tool disclosure and final report structure. | **Present**, although presentation/defence material itself is outside the technical report. |
| **What makes it convincing/complete** | End-to-end architecture + quantitative KPIs + energy model \+ economics + deployment roadmap. | **Very strong** |

### Overall mapping

 P1 covers **essentially every element of the template**.

 The strongest aspect is that the project connects the technical layers rather than treating them independently:

 > **Acoustic sensing → local AI → low-power communication → gateway → cloud → dashboard → deployment → cost model → commercial product.**

 That makes the project coherent as an IoT system rather than just a collection of component-selection exercises.

---

 # TD3 — How P1 fulfills the official project guidelines

 Based on the project structure represented in P1, the document can be evaluated against the typical requirements of an IoT engineering project.

 ## 1\. Problem definition

 **Fulfilled.**

 P1 establishes a concrete real-world application: continuous environmental acoustic monitoring. The project is sufficiently specific to define measurable engineering requirements.

 The use case also naturally justifies IoT characteristics such as:

 - distributed sensing;
- low-power operation;
- wireless connectivity;
- cloud storage;
- remote monitoring;
- automated classification;
- scalable deployment.

 This is an appropriate IoT problem because the system's value comes from connecting many physical sensing devices to centralized processing and user-facing services.

---

 ## 2\. Requirements engineering

 **Strongly fulfilled.**

 P1 goes considerably beyond a qualitative list of requirements.

 The appendices provide quantitative targets such as:

 - approximately 50-byte average payload;
- configurable 30–300 s uplink interval;
- approximately 100 kB/device/day;
- \<50 ms on-device inference;
- P95 end-to-end latency \<30 s;
- PDR ≥95%;
- Macro-F1 ≥0.85;
- ±1.5 dB measurement accuracy at the specified calibration point;
- 400–500 nodes/gateway planning capacity;
- 99.9% cloud-service availability target.

 This is exactly the type of quantitative specification expected in a serious engineering project.

 ### Improvement

 The requirements would be stronger if they were explicitly classified as:

 - **functional requirements**;
- **performance requirements**;
- **constraints**;
- **acceptance criteria**.

 For example:

 | ID | Requirement | Type | Verification |
| --- | --- | --- | --- |
| FR-01 | Measure environmental acoustic levels | Functional | Test |
| PR-01 | PDR ≥95% over 24 h | Performance | Field test |
| PR-02 | Macro-F1 ≥0.85 | Performance | Dataset evaluation |
| PR-03 | P95 E2E latency \<30 s | Performance | System test |
| C-01 | Outdoor node operates from solar + battery | Constraint | Energy test |

That would make the requirements traceable to validation.

---

 # 3\. IoT architecture

 **Very strongly fulfilled.**

 The architecture is one of the clearest aspects of P1.

 It effectively follows:

 **Device → Gateway → Cloud → User**

 with AI processing occurring close to the sensing device.

 This provides:

 - physical sensing;
- local computation;
- wireless networking;
- centralized data management;
- analytics;
- visualization.

 The architecture is also scalable because the gateway abstracts hundreds of sensor nodes from the cloud backend.

 ### Improvement

 The report would benefit from one explicit **end-to-end architecture diagram** showing:

```
MEMS microphone
       ↓
   MCU / TinyML
       ↓
   LoRa node
       ↓
   LoRa gateway
       ↓
Cloud ingestion/API
       ↓
Database + analytics
       ↓
Web / mobile dashboard
       ↓
University / municipality
```

 The individual elements are already present; the improvement would mainly be visual integration.

---

 # 4\. Hardware engineering

 **Very strongly fulfilled.**

 P1 provides actual component-level engineering rather than merely naming technologies.

 It addresses:

 - microphone selection;
- MCU alternatives;
- radio alternatives;
- PMIC;
- battery;
- solar panel;
- enclosure;
- gateway;
- indoor/outdoor variants.

 Appendix C is particularly useful because it documents alternatives instead of pretending there was only one possible component.

 The project therefore demonstrates **engineering trade-off analysis**.

---

 # 5\. Communication

 **Strongly fulfilled.**

 The communication architecture is quantitatively specified.

 P1 provides:

 - LoRa/LPWAN communication;
- approximately 2 km outdoor range target;
- several-hundred-meter indoor range target;
- ≥95% PDR;
- packet-loss definition;
- gateway capacity;
- channel occupancy;
- local buffering;
- sent-uplink counters for reconciliation.

 This is good engineering practice because communication performance is connected to measurable acceptance criteria.

---

 # 6\. Software

 **Fulfilled across all major layers.**

 P1 addresses:

 ### Embedded

 - sensor acquisition;
- feature processing;
- TinyML inference;
- data packaging;
- power management;
- wireless transmission.

 ### Cloud

 - ingestion;
- processing;
- alert rules;
- database;
- storage;
- APIs/backend.

 ### Frontend

 - web dashboard;
- mobile interface;
- recent measurements;
- maps/time series;
- customer-facing monitoring.

 The software architecture therefore matches the hardware architecture rather than existing as an independent component.

---

 # 7\. AI / EdgeAI

 **Strongly fulfilled.**

 The project has a legitimate EdgeAI use case.

 Instead of continuously transmitting raw audio, the node processes acoustic information locally and transmits compact information.

 The report defines:

 - 1-second decision windows;
- majority voting over five windows;
- Macro-F1 ≥0.85;
- confidence threshold `p < 0.60 → unknown`;
- inference target \<50 ms/frame.

 This is particularly important because EdgeAI is tied to the project's energy and communication constraints.

 It is not AI included merely for presentation value; it has a systems-level purpose.

---

 # 8\. Energy engineering

 **Very strongly fulfilled.**

 Appendix B gives a numerical power model.

 The report calculates:

 $$
I_{\mathrm{tot}}\approx2.93\text{ mA}
$$

 and:

 $$
P_{\mathrm{avg}}
=I_{\mathrm{tot}}V_{\mathrm{batt}}
\approx2.93\text{ mA}\times3.7\text{ V}
\approx10.8\text{ mW}.
$$

 It then connects this to:

 - battery capacity;
- autonomy;
- solar generation;
- winter conditions;
- recharge time;
- outdoor deployment.

 This is a major strength because the energy analysis is directly connected to the physical deployment scenario.

---

 # 9\. Cloud architecture

 **Strongly fulfilled.**

 P1 specifies:

 - ingestion;
- processing;
- alerts;
- database;
- query performance;
- storage footprint;
- availability;
- multi-tenant isolation.

 The report even gives a storage estimate of approximately 3.6 GB/year for 100 devices and defines an insertion-rate target.

 That makes the cloud portion quantitatively grounded.

---

 # 10\. PoC and implementation

 **Partially/strongly fulfilled, with an important distinction.**

 P1 clearly defines a **10-node pilot** and a subsequent **500-node commercial deployment**.

 However, the document sometimes moves between:

 - what has actually been implemented;
- what has been validated;
- what has been estimated;
- what is planned for future deployment.

 Those categories should be explicitly separated.

 For example:

 | Status | Meaning |
| --- | --- |
| **Implemented** | Actually built and demonstrated |
| **Tested** | Experimentally measured |
| **Simulated/calculated** | Derived analytically |
| **Target** | Required future performance |
| **Planned** | Intended commercial implementation |

This is probably the **single most important structural improvement** I would make to P1.

 It prevents a reviewer from interpreting an engineering estimate as an experimental result.

---

 # 11\. Testing and validation

 **Good, but this is where P1 could become substantially stronger.**

 There are many KPIs and validation criteria, but some of the text uses terms such as:

 - "estimated";
- "target";
- "nominal";
- "expected";
- "planning";
- "approximately."

 That is perfectly legitimate for engineering design, but a final academic project should distinguish **predicted performance from measured performance**.

 For example:

 > Target: Macro-F1 ≥ 0.85

 is different from:

 > Measured: Macro-F1 = 0.87 on dataset X.

 Likewise:

 > Target PDR ≥95%

 is different from:

 > Measured PDR = 96.8% over a 24-hour campus test.

 ### Recommended validation matrix

 A strong final version could include:

 | Requirement | Target | Measured result | Pass? | Test method |
| --- | --- | --- | --- | --- |
| PDR | ≥95% | XX% | Yes/No | 24-h field test |
| Inference | \<50 ms | XX ms | Yes/No | MCU benchmark |
| Macro-F1 | ≥0.85 | XX | Yes/No | Held-out dataset |
| E2E latency | P95 \<30 s | XX s | Yes/No | End-to-end test |
| Power | 10.8 mW target | XX mW | Yes/No | Current measurement |
| Acoustic accuracy | ±1.5 dB | XX dB | Yes/No | Calibrator test |

That would transform the KPI appendix into a genuine **requirements-verification matrix**.

---

 # 12\. Business and scalability

 **Exceptionally well covered.**

 This is arguably one of the most complete portions of P1.

 The document includes:

 - NRE;
- personnel;
- overhead;
- equipment;
- certification;
- TCO;
- pilot economics;
- 500-node economics;
- subscription model;
- pricing;
- unit economics;
- break-even;
- commercialization roadmap;
- scaling assumptions.

 The progression is logical:

 **Prototype → pilot → early customers → 500-node deployment → recurring service → larger-scale commercialization.**

 That directly addresses whether the proposed IoT system can become a product rather than stopping at a technical prototype.

---

 # 13\. Project planning

 **Fulfilled.**

 The 24-month GANTT and milestones provide a development roadmap.

 The final stages explicitly identify:

 - manufacturing readiness;
- commercial launch.

 That connects the technical work to project management and commercialization.

---

 # 14\. Team roles

 **Fulfilled.**

 The final section explicitly documents the contribution of the three team members and divides responsibilities among:

 - device/general architecture;
- UI/AI;
- cloud/financial analysis.

 This is useful for demonstrating individual contribution.

 One possible improvement would be to map each person's work to specific report sections, implementation artefacts and deliverables.

---

 # 15\. AI-tool disclosure

 **Fulfilled.**

 P1 explicitly states how:

 - ChatGPT;
- Perplexity;
- Gemini

 were used.

 This is preferable to simply mentioning that AI was used because it explains the role of each tool.

 A stronger version would additionally distinguish:

 > **AI-assisted work** vs. **human-verified technical decisions/results**.

 For example, component specifications, calculations, experimental results and references should be explicitly treated as human-verified outputs rather than accepted solely because an AI system produced them.

---

 # Overall TD3 assessment

 P1 **substantially fulfills the expected structure of a complete IoT engineering project**.

 Its coverage can be summarized as:

 | Area | Coverage |
| --- | --- |
| Problem/use case | **Strong** |
| Requirements | **Very strong** |
| Architecture | **Very strong** |
| Hardware | **Very strong** |
| Communications | **Very strong** |
| Embedded software | **Strong** |
| EdgeAI | **Very strong** |
| Cloud | **Strong** |
| Energy | **Very strong** |
| Data flow | **Strong** |
| PoC | **Present; implementation status should be clearer** |
| Testing/validation | **Good; measured vs. estimated results need separation** |
| Business model | **Very strong** |
| Cost/TCO | **Very strong** |
| Scalability | **Very strong** |
| Project planning | **Strong** |
| Team contribution | **Present** |
| AI disclosure | **Present** |

## The main strengths of P1

 The project is particularly convincing because it closes several loops that are often missing in IoT projects:

 **Technical loop**

 > Sensor → MCU → AI → LoRa → Gateway → Cloud → UI

 **Energy loop**

 > Power consumption → battery → solar harvesting → autonomy → deployment feasibility

 **Performance loop**

 > Requirements → KPIs → calculations/tests → validation

 **Economic loop**

 > Component costs → NRE → TCO → price → break-even → commercialization

 **Project-management loop**

 > Development phases → GANTT → pilot → industrialization → commercial launch

 That combination makes P1 much closer to a **complete product/system engineering proposal** than a conventional prototype report.
