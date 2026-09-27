 # TD1 — Derived structure of Project 1

 The project is structured as a complete **IoT product-development proposal/design report** for **EchoSense**, an environmental acoustic-monitoring platform.

 At the highest level, P1 follows this logic:

 1. **Problem definition and motivation**
   - Continuous environmental/acoustic noise monitoring.
   - Need for scalable, distributed monitoring rather than isolated/manual measurements.
   - Target deployment in campuses and municipalities.
2. **System requirements and KPIs**
   - Acoustic measurement accuracy.
   - Classification performance.
   - Communication range and reliability.
   - Energy autonomy.
   - Latency.
   - Cloud performance.
   - Mechanical/environmental constraints.
   - Cost and scalability.
3. **System architecture**
   - Distributed sensing nodes.
   - Wireless/LPWAN communication.
   - Gateways.
   - Cloud backend.
   - Web/mobile dashboards.
   - AI/TinyML processing at the device/edge.
4. **Hardware design**
   - MEMS microphone.
   - MCU/SoC.
   - LoRa/sub-GHz radio.
   - Power-management circuitry.
   - Battery.
   - Solar harvesting for outdoor nodes.
   - Indoor/outdoor enclosures.
5. **Embedded/EdgeAI**
   - Audio acquisition.
   - Feature extraction.
   - On-device classification.
   - Decision smoothing.
   - Uncertainty handling.
6. **Communication and networking**
   - LoRa/LPWAN-class communication.
   - Gateway infrastructure.
   - PDR/loss measurement.
   - Node capacity.
   - Local buffering.
7. **Cloud and user interface**
   - Data ingestion.
   - Processing and alert rules.
   - Database/storage.
   - APIs/backend.
   - Web/mobile dashboards.
   - Multi-tenant architecture.
8. **Energy and performance analysis**
   - Current consumption by subsystem.
   - Duty cycles.
   - Average current.
   - Average power.
   - Battery autonomy.
   - Solar sizing and winter margin.
9. **Implementation and validation**
   - Prototype/design implementation.
   - Performance targets.
   - Testing and certification.
   - Pilot deployment.
   - Manufacturing readiness.
10. **Commercialization**
    - NRE calculation.
    - Direct/indirect costs.
    - TCO.
    - Pricing.
    - Business model.
    - Break-even.
    - Scaling to 500-node campuses.
11. **Project planning**
    - 24-month GANTT.
    - Milestones M7 and M8.
    - Manufacturing readiness.
    - Commercial launch.
12. **Conclusion and project accountability**
    - Technical conclusions.
    - Economic conclusions.
    - Team roles.
    - AI-tool usage.
    - References.
    - KPI and component-selection appendices.

 So the overall P1 story is essentially:

 **Problem → requirements → architecture → hardware/software → AI → communication → energy → implementation/validation → economics → commercialization.**

---

 # TD2 — Mapping P1 against the required template

 | Required template element | Where/how P1 addresses it | Assessment |
| --- | --- | --- |
| **Problem / use case** | EchoSense provides continuous environmental acoustic monitoring, particularly for campuses and municipalities. | **Strongly covered** |
| **Target users and stakeholders** | Universities, municipalities, campus operators, customers, technical/operations personnel. | **Covered**, although stakeholder roles could be made more explicit |
| **Requirements** | Detailed KPI appendix: payload, uplink interval, latency, acoustic accuracy, frequency response, Macro-F1, PDR, energy, temperature, cloud SLOs, cost, etc. | **Very strongly covered** |
| **Market/context analysis** | Existing environmental sensing solutions, commercial positioning, competitive pricing, target B2B customers and early adopters. | **Covered**, but could benefit from a more explicit competitor/market comparison |
| **IoT architecture** | Device → wireless/LoRa → gateway → cloud/backend → web/mobile UI. | **Very strongly covered** |
| **Hardware** | MEMS microphone, ESP32-S3/alternative MCUs, SX1262/LPWAN radio, battery, solar panel, PMIC, enclosure, gateways. | **Very strongly covered** |
| **Communication** | Sub-GHz LPWAN/LoRa, range, PDR, packet-loss definition, gateway capacity, channel occupancy, buffering. | **Very strongly covered** |
| **Software** | Embedded firmware, TinyML, cloud backend, database, dashboard/web/mobile interfaces. | **Covered** |
| **Data flow** | Acoustic acquisition → feature processing/classification → compact uplink payload → gateway → cloud ingestion → processing/storage → dashboard. | **Covered**, though an explicit data-flow diagram would strengthen it |
| **AI / EdgeAI** | TinyML classifier, 1-s windows, majority voting, Macro-F1 ≥ 0.85, uncertainty threshold. | **Very strongly covered** |
| **Energy/performance** | Detailed current/duty-cycle table, 10.8 mW calculation, 11 Wh battery, solar sizing, winter margin and recharge. | **Excellent coverage** |
| **Cloud architecture** | Ingestion, processing, alerts, database/storage, query performance, availability, scaling and multi-tenancy. | **Strongly covered** |
| **PoC / actual implementation** | Prototype/implementation planning, pilot deployment, 10-node pilot, component selections, implementation options, validation targets. | **Partially/strongly covered**, but distinction between implemented vs planned components should be clearer |
| **Business model, costs, scalability** | NRE, overhead, TCO, pricing, 500-node campus, 7,500-node/15-customer assumption, break-even. | **Excellent coverage** |
| **Testing and validation** | KPI targets, acoustic calibration, PDR measurement, latency, classifier Macro-F1, energy calculations, certification. | **Strongly covered** |
| **Reports/presentations/defence** | Report itself, GANTT, roles, AI tools, appendices and references. | **Partially covered**; presentation/defence strategy is not really a substantive technical section |
| **What makes project convincing/complete** | Technical + economic integration, quantitative KPIs, architecture, implementation planning and commercialization. | **Strong** |
| **What could be improved** | Several claims are presented as targets/estimates rather than experimentally demonstrated results; some references and tables are incomplete/corrupted in the supplied version. | **Main improvement area** |

---

 # 1\. Problem / use case

 P1 clearly establishes **environmental acoustic monitoring** as the central use case.

 EchoSense is not simply an audio recorder. The intended system performs:

 **sound sensing → acoustic measurement → classification → wireless transmission → cloud analytics → visualization/alerts.**

 The target deployment scenario is particularly clear in the commercial section:

 - pilot: **10 nodes**
- commercial campus: **500 nodes**
- outdoor/indoor mixture
- approximately **8–10 gateways**
- multi-year cloud/service operation

 This is a good match to an IoT project because the problem inherently requires **distributed physical sensing plus connectivity and centralized processing**.

 ### Strength

 The use case is connected to an actual deployment scenario rather than being presented only as a laboratory prototype.

---

 # 2\. Target users and stakeholders

 P1 identifies:

 - **Universities**
- **Municipalities**
- Campus operators/customers
- Early-adopter institutions
- Technical/operations personnel
- End users of the web/mobile dashboards

 The commercial model explicitly describes universities and municipalities as B2B customers.

 ### What could be improved

 The stakeholder structure could be made more explicit:

 | Stakeholder | Need |
| --- | --- |
| University/municipality | Environmental monitoring and reporting |
| Campus/environment manager | Operational dashboard and alerts |
| Technical operator | Device health and diagnostics |
| Management | Long-term trends and reports |
| Research/AI team | Acoustic data and classification |
| Installer | Straightforward deployment and commissioning |
| End user | Accessible visualization |

This would make the project easier to understand from a systems-engineering perspective.

---

 # 3\. Requirements

 This is one of P1's strongest areas.

 Appendix A essentially provides a **requirements/KPI specification**.

 Examples include:

 - Payload: approximately **50 B**
- Configurable uplink: **30–300 s**
- Typical uplink interval: **60 s**
- On-device feature frame: **1 s**
- Inference time: **\<50 ms/frame**
- E2E latency: **P95 \<30 s**
- Acoustic accuracy: **±1.5 dB @ 94 dB SPL, 1 kHz**
- Linearity: **±1 dB over 40–100 dB SPL**
- Classifier: **Macro-F1 ≥0.85**
- PDR: **≥95%**
- Outdoor range: approximately **2 km typical**
- Gateway planning capacity: approximately **400–500 nodes**
- Outdoor average power: **10.8 mW**
- Service availability target: **99.9%**
- Storage: approximately **3.6 GB/year for 100 devices**

 This is exactly the sort of quantitative specification expected from a serious engineering project.

---

 # 4\. Market/context analysis

 P1 does address the commercial context.

 The report positions EchoSense as a solution for:

 - universities,
- municipalities,
- campus-scale installations,
- environmental sensing,
- recurring cloud/service contracts.

 It also discusses existing environmental sensing solutions and derives a commercial price.

 The commercial model is:

 **hardware sale + installation \+ recurring cloud/analytics/support service.**

 The proposed 500-node package is approximately **€100,000 for three years**, while a pilot is estimated at **€9,000–€10,000 for one year**.

 ### Improvement

 The market analysis would be stronger if it explicitly contained a table such as:

 | Existing approach | Strength | Limitation | EchoSense differentiation |
| --- | --- | --- | --- |
| Manual acoustic surveys | Accurate/local | Not continuous | Continuous monitoring |
| Conventional sound meters | Mature measurement | Limited spatial scalability | Distributed IoT network |
| Generic IoT sensors | Cheap/connectivity | May lack acoustic specialization | Acoustic + TinyML |
| Commercial environmental platforms | Integrated | Potentially expensive | Campus-scale customizable platform |

That would make the competitive positioning much easier to defend.

---

 # 5\. IoT architecture

 P1 strongly satisfies the IoT architecture requirement.

 The implied architecture is:

```
┌──────────────────────┐
│ Device / Sensor Node │
│                      │
│ MEMS microphone      │
│ MCU + TinyML         │
│ LoRa radio           │
│ Battery / Solar      │
└──────────┬───────────┘
           │
           │ LoRa / LPWAN
           ▼
┌──────────────────────┐
│       Gateway        │
└──────────┬───────────┘
           │
           │ IP / Internet
           ▼
┌──────────────────────┐
│    Cloud Platform    │
│                      │
│ Ingestion             │
│ Processing            │
│ Database              │
│ APIs                  │
│ Analytics             │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ Web / Mobile UI      │
│                      │
│ Metrics              │
│ Maps                 │
│ Alerts               │
│ Reports              │
└──────────────────────┘
```

 This maps almost perfectly to the template's:

 **Device → Edge/Mobile → Cloud → User**

 with the gateway inserted between device and cloud.

---

 # 6\. Hardware

 Hardware coverage is extensive.

 The report discusses:

 ### Sensing

 - ICS-43434 MEMS microphone
- I2S digital interface
- approximately 0.6 mA microphone current

 ### Processing

 - ESP32-S3
- alternative MCU/SoC options
- TinyML processing

 ### Communications

 - SX1262-class LoRa radio
- sub-GHz LPWAN
- alternative wireless approaches

 ### Power

 - Li-ion battery
- approximately 11 Wh outdoor battery
- approximately 2 Wp solar panel
- PMIC
- regulators

 ### Mechanical

 - IP65 outdoor enclosure
- IP40 indoor enclosure
- ASA/polycarbonate options
- environmental temperature limits

 ### Gateway

 The appendix considers:

 - dedicated long-range gateways
- SBC-based gateways
- infrastructure-based indoor gateways

 This is a very comprehensive hardware treatment.

---

 # 7. Communication

 Communication is particularly well specified.

 P1 defines:

 - sub-GHz LPWAN communication,
- approximately 2 km outdoor range,
- several hundred meters indoor,
- PDR ≥95%,
- packet-loss definition,
- gateway capacity,
- channel occupancy,
- local buffering,
- no retransmissions,
- periodic control messages for estimating loss.

 The specification:

 > Loss = 1 − PDR

 combined with gateway counters and cloud reconciliation gives a concrete measurement methodology rather than simply stating "reliable communication."

 That's a significant strength.

---

 # 8\. Software

 The software architecture covers three major layers.

 ### Embedded

 - sensor acquisition,
- feature extraction,
- TinyML inference,
- communication,
- power management,
- buffering.

 ### Cloud

 - ingestion,
- processing,
- alert rules,
- storage/database,
- APIs,
- multi-tenant backend.

 ### User interface

 - web dashboard,
- mobile interface,
- maps,
- recent time series,
- monitoring and reporting.

 The report therefore addresses both the **device software** and the **platform software**.

---

 # 9\. Data flow

 The complete data path can be reconstructed as:

```
Acoustic environment
        ↓
MEMS microphone
        ↓
1 s audio/features
        ↓
TinyML inference
        ↓
Class + confidence + acoustic metrics
        ↓
Compact binary payload
        ↓
LoRa/LPWAN
        ↓
Gateway
        ↓
Cloud ingestion
        ↓
Processing / alert rules
        ↓
Database
        ↓
API
        ↓
Web/mobile dashboard
        ↓
User
```

 The report also specifies approximately **50 B average payload size** and approximately **100 kB/device/day including protocol overhead**.

 ### Improvement

 A single dedicated **"End-to-End Data Flow"** diagram would make this much easier to communicate during a defence.

---

 # 10\. AI / EdgeAI

 This is another strong area.

 P1 doesn't merely mention AI; it defines an operational TinyML pipeline.

 Key parameters:

 - 1-second decision windows
- minimal overlap
- majority voting over five windows
- Macro-F1 ≥0.85
- confidence threshold
- predictions with **p \< 0.60 → unknown**
- inference target \<50 ms/frame

 This demonstrates that AI is integrated into the system architecture rather than added as a superficial feature.

 The use of EdgeAI also supports the project's communication and energy strategy because raw audio does not need to be continuously transmitted.

---

 # 11\. Energy and performance

 P1 provides unusually detailed energy modeling.

 The outdoor-node calculation is:

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

 It then translates this into:

 - approximately 11 Wh battery,
- approximately 43 days autonomy without solar,
- approximately 2 Wp solar input,
- winter energy margin ≥25%.

 This connects the component-level electrical analysis to system-level deployment.

 That is exactly the kind of chain a technical evaluator can follow:

 **component current → average current → average power → battery → autonomy → solar sizing.**

---

 # 12\. Cloud architecture

 The cloud section is also well represented.

 P1 specifies:

 - ingestion,
- processing,
- alert rules,
- recent-metric queries,
- database/storage,
- availability,
- insertion rate,
- storage footprint,
- multi-tenant isolation.

 Examples:

 - processing/alert SLO: **\<500 ms after data arrival**
- recent metrics: **\<2 s**
- service availability target: **99.9%**
- storage: approximately **3.6 GB/year for 100 devices**

 The report therefore connects cloud architecture to measurable performance requirements.

---

 # 13\. PoC and actual implementation

 This is one area where I would recommend making a stronger distinction.

 P1 describes:

 - the prototype/design,
- component selection,
- implementation planning,
- pilot deployment,
- 10-node pilot,
- validation criteria,
- industrialization,
- certification.

 However, throughout the supplied material, some numbers are clearly **targets, estimates or design assumptions**, rather than demonstrated measurements.

 For example:

 - Macro-F1 ≥0.85 is a target.
- PDR ≥95% is a target.
- 10.8 mW is a calculated estimate.
- 2 km is a planning/range specification.
- 99.9% is a cloud availability target.
- 500 nodes/gateway is a planning capacity.

 For a defence, the report should explicitly classify every important result as one of:

 **Measured / Simulated / Calculated / Estimated / Target / Planned.**

 That would eliminate ambiguity.

---

 # 14\. Business model, costs and scalability

 This is one of P1's strongest sections.

 The report explicitly separates:

 ### Fixed costs

 - NRE
- engineering
- certification
- equipment
- overhead

 ### Variable/deployment costs

 - hardware
- gateways
- installation
- cloud
- operations/support

 The NRE calculation is:

 $$
24\text{ person-months}
$$

 with direct labor:

 $$
€180,500.
$$

 Then:

 $$
20\%\text{ overhead}=€36,100
$$

 plus:

 - €6,000 test equipment/jigs
- €12,000 certification

 giving:

 $$
\boxed{NRE=€234,600}.
$$

 The report then amortizes NRE over the assumed initial commercial volume.

 For the 500-node campus:

 $$
TCO_{\text{3yr}}=€68,900
$$

 before contingency, and approximately:

 $$
\boxed{€79,200}
$$

 including the 15% contingency.

 The proposed selling price is approximately:

 $$
\boxed{€100,000}
$$

 for 500 nodes and three years of service.

 The report then calculates a break-even deployment volume of approximately:

 $$
\boxed{6.4\text{ campuses}}
$$

 using its stated assumptions.

 This is a very complete progression:

 **engineering cost → deployment cost → TCO → selling price → contribution → break-even → scalability.**

---

 # 15\. Testing and validation

 P1 provides a substantial validation framework.

 It includes:

 - acoustic accuracy,
- frequency response,
- calibration,
- classifier Macro-F1,
- inference time,
- end-to-end latency,
- PDR,
- packet loss,
- gateway capacity,
- cloud query performance,
- cloud availability,
- energy consumption,
- battery autonomy,
- environmental operating range,
- certification.

 The annual field-verification concept and reference to ISO 1996-1 also give the acoustic measurement part a standards-oriented basis.

 ### Improvement

 The report would benefit from a dedicated validation matrix:

 | Requirement | Target | Test method | Result | Status |
| --- | --- | --- | --- | --- |
| Acoustic accuracy | ±1.5 dB | Calibrated source | X | Pass/Fail |
| PDR | ≥95% | 24-h field test | X | Pass/Fail |
| Macro-F1 | ≥0.85 | Held-out dataset | X | Pass/Fail |
| Inference | \<50 ms | Device benchmark | X | Pass/Fail |
| Latency | P95 \<30 s | E2E test | X | Pass/Fail |
| Autonomy | 43 days no solar | Energy calculation/test | X | Pass/Fail |

That would make the difference between **specification** and **validation evidence** immediately visible.

---

 # 16\. Reports, presentations and defence

 P1 is clearly written as a formal engineering report and contains:

 - main technical sections,
- tables,
- figures,
- references,
- appendices,
- GANTT,
- roles/contributions,
- AI-tool declaration,
- conclusion.

 However, the **presentation/defence structure is not explicitly developed** in the document.

 For the defence, I would extract the project into approximately this narrative:

 1. **Problem:** Why environmental acoustic monitoring matters.
2. **Solution:** What EchoSense is.
3. **Architecture:** Device → Gateway → Cloud → UI.
4. **Node:** Hardware + energy.
5. **AI:** TinyML classification.
6. **Communication:** LoRa + reliability.
7. **Cloud:** ingestion → database → dashboard.
8. **Validation:** KPI evidence.
9. **Economics:** €79.2k internal 3-year cost vs. \~€100k package.
10. **Scalability:** 10-node pilot → 500-node campus.
11. **Roadmap:** manufacturing → launch.
12. **Conclusion:** technical + economic feasibility.

 That is a much more efficient defence narrative than presenting the report chapter-by-chapter.

---

 # TD3 — How well P1 fulfills the official project structure

 Taking the template you provided as the official structure, P1 is **very comprehensive**.

 I would characterize the coverage as follows—not as a score, but as a structural assessment:

 | Area | P1 coverage |
| --- | --- |
| Problem/use case | **Explicit** |
| Users/stakeholders | **Explicit but could be expanded** |
| Requirements | **Highly explicit** |
| Market/context | **Present** |
| IoT architecture | **Highly explicit** |
| Hardware | **Highly explicit** |
| Communication | **Highly explicit** |
| Software | **Explicit** |
| Data flow | **Present, but could be visualized better** |
| AI/EdgeAI | **Highly explicit** |
| Energy | **Highly explicit and quantitative** |
| Cloud | **Explicit and quantitative** |
| PoC | **Present, but implementation evidence should be separated from targets** |
| Business model | **Highly explicit** |
| Costs/TCO | **Highly explicit** |
| Scalability | **Explicit** |
| Testing/validation | **Explicit, but evidence/result separation should improve** |
| Planning | **Explicit via GANTT/milestones** |
| Team/roles | **Explicit** |
| References | **Present, but formatting/content needs cleanup** |
| Appendices | **Extensive** |

## The overall structure of P1

 If I compress the entire project into the template, the resulting structure is:

```
PROJECT 1 — ECHOSENSE
│
├── 1. Problem / Use Case
│   └── Environmental acoustic monitoring
│
├── 2. Users / Stakeholders
│   ├── Universities
│   ├── Municipalities
│   └── Campus/environment operators
│
├── 3. Requirements / KPIs
│   ├── Acoustic
│   ├── AI
│   ├── Communication
│   ├── Energy
│   ├── Cloud
│   └── Mechanical
│
├── 4. Market / Context
│   ├── Existing solutions
│   ├── Target market
│   └── Commercial positioning
│
├── 5. IoT Architecture
│   └── Device → Gateway → Cloud → UI
│
├── 6. Hardware
│   ├── MEMS microphone
│   ├── MCU
│   ├── LoRa radio
│   ├── PMIC
│   ├── Battery
│   ├── Solar
│   └── Enclosure
│
├── 7. Communication
│   ├── LoRa/LPWAN
│   ├── Range
│   ├── PDR
│   ├── Gateway capacity
│   └── Buffering
│
├── 8. Software
│   ├── Firmware
│   ├── TinyML
│   ├── Backend
│   ├── Database/API
│   └── Web/mobile UI
│
├── 9. Data Flow
│   └── Acoustic data → inference → LoRa → cloud → UI
│
├── 10. AI / EdgeAI
│   ├── Feature extraction
│   ├── Classification
│   ├── Macro-F1
│   └── Confidence handling
│
├── 11. Energy / Performance
│   ├── Current model
│   ├── Battery
│   ├── Solar
│   └── Autonomy
│
├── 12. Cloud
│   ├── Ingestion
│   ├── Processing
│   ├── Storage
│   ├── APIs
│   └── Dashboard
│
├── 13. PoC / Implementation
│   ├── Prototype
│   ├── Pilot
│   └── Validation
│
├── 14. Testing / Validation
│   ├── Acoustic
│   ├── AI
│   ├── Network
│   ├── Energy
│   └── Cloud
│
├── 15. Business / Economics
│   ├── NRE
│   ├── TCO
│   ├── Pricing
│   ├── Business model
│   └── Break-even
│
├── 16. Scaling / Commercialization
│   ├── 10-node pilot
│   ├── 100–500-node deployments
│   └── 500-node campus
│
├── 17. Project Planning
│   ├── GANTT
│   ├── M7 Manufacturing readiness
│   └── M8 Commercial launch
│
├── 18. Roles / AI Tools
│
├── 19. References
│
└── 20. Appendices
    ├── KPI summary
    ├── Power calculations
    ├── Component alternatives
    └── GANTT
```

 # Most important gaps/improvements in P1

 The project is structurally complete, but there are a few things I would fix before treating it as a final submission.

 ### 1\. Separate "target" from "achieved"

 This is probably the **single most important technical improvement**.

 The report sometimes moves from:

 > target/specification

 to:

 > "meets" / "validated"

 without always showing the corresponding experimental evidence.

 Use explicit labels:

 - **Requirement**
- **Design calculation**
- **Simulation**
- **Prototype measurement**
- **Experimental result**
- **Planned future validation**

 That makes the engineering argument much more defensible.

 ### 2\. Make the PoC status explicit

 A reviewer should immediately understand:

 > What did we actually build?

 versus:

 > What did we design?

 versus:

 > What is proposed for future industrialization?

 A one-page **PoC implementation summary** would solve this.

 ### 3\. Add a requirements-to-evidence matrix

 This would connect almost the entire project:

 $$
\text{Requirement}
\rightarrow
\text{Design}
\rightarrow
\text{Test}
\rightarrow
\text{Result}
\rightarrow
\text{Pass/Fail}
$$

 It would also make the defence much easier.

 ### 4\. Strengthen the market analysis

 The economics are detailed, but the **market evidence** is less detailed than the engineering evidence.

 A concise competitor/context table would improve this substantially.

 ### 5\. Clean the references

 The supplied reference section contains visibly corrupted/incomplete entries such as:

 - "\[2\] Available:"
- "\[4\] l Sensor."
- "\[19\] Kerliivity networks..."
- "\[20\] ChirpStack ProjSource..."
- several missing titles/URLs.

 This is a clear presentation-quality issue and should be fixed before submission.

 ### 6\. Reconcile terminology and numerical assumptions

 There are a few places where the document should be checked for consistency, particularly:

 - BOM values versus selling-price calculations,
- NRE amortization versus the stated 15-campus/7,500-node assumption,
- "3.2× BOM" unit pricing versus the 3-year campus package,
- gateway count versus the 400–500 nodes/gateway planning value,
- calculated power versus the energy/autonomy assumptions.

 The underlying approach is coherent, but these relationships should be explicitly reconciled so a reviewer cannot challenge them based on apparent inconsistencies.

 ### 7. Improve the defence-oriented diagrams

 Three diagrams would make the whole project immediately understandable:

 1. **System architecture**
2. **End-to-end data flow**
3. **Requirement → validation → result**

 The existing GANTT and break-even diagrams already cover planning/economics.

---
