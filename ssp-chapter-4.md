Yes. Your concern is correct, and this is important enough that I would **not yet freeze Chapter 4**.

 The current Chapter 4 is substantially stronger than the earlier version, but there is a structural weakness: **we have defined many functional requirements with F- identifiers, while most performance requirements are expressed as prose targets without P- identifiers and without being systematically organized by system layer.**

 That does not mean the technical content is missing. Much of it is already there. The problem is **traceability and completeness of the specification**.

 ## 1\. Should each layer have both F- and P- requirements?

 **Yes, generally.**

 For SSP, the cleanest model is:

 | Layer/subsystem | Functional requirements | Performance requirements |
| --- | --- | --- |
| Device | F-D01…F-D12 | P-Dxx |
| Edge | F-E01…F-E15 | P-Exx |
| Communication | F-C01…F-C12 | P-Cxx |
| Cloud | F-CL01…F-CL19 | P-CLxx |
| UI | F-U01…F-U13 | P-Uxx |

Then there are **cross-system performance requirements** that do not belong exclusively to one layer:

 - P-Sxx — system/end-to-end performance
- P-SECxx — security, if we decide security performance needs measurable targets
- P-PRVxx — privacy/data-minimization performance
- P-AIxx — AI performance
- P-ECxx — economic performance

 We don't necessarily need all of those prefixes. The important thing is that the convention is systematic and traceable.

 ### But there is an important nuance

 We **do not need a one-to-one P requirement for every F requirement**.

 For example:

 > F-D02 — Position determination

 can be complemented by several performance requirements:

 > P-D01 — Position update rate\
>  P-D02 — Positioning latency\
>  P-D03 — Positioning energy consumption\
>  P-D04 — Position confidence

 Likewise:

 > F-E08 — Event evaluation

 could be complemented by:

 > P-E01 — Edge event-evaluation latency\
>  P-E02 — Edge processing throughput

 So the correct relationship is:

 **Functional requirement → one or more measurable performance requirements**

 rather than:

 **F-D01 → P-D01 → F-D02 → P-D02**

 That distinction is important.

---

 # 2\. Is it difficult to define P-requirements?

 No. **Technically, most of them are already present in our Chapter 4.**

 The work is primarily to reorganize and make the existing numbers explicit.

 For example, we already have:

 > sensor-acquisition latency ≤20 ms

 > local preprocessing latency ≤100 ms

 > local event-rule evaluation ≤200 ms

 > event-decision generation ≤500 ms

 > average processing duty cycle ≤20%

 Those are clearly **P-D requirements**.

 Similarly, we already have:

 > device-to-edge application latency ≤2 s

 > communication capacity ≥100 kbit/s

 > nominal range ≥10 m

 > communication latency ≤500 ms

 Those are **P-C requirements**.

 And:

 > battery autonomy ≥7 days

 > deep-sleep power ≤1 mW

 > normal-monitoring average power ≤50 mW

 are clearly **P-D energy requirements**.

 So we are not inventing a second specification. We are **properly structuring the specification we already developed**.

---

 # 3\. Does the current Chapter 4 answer the official questions?

 I would assess it as follows.

 ## A. "Are all the possible functions at device, edge, cloud & UI well defined?"

 ### **Yes — substantially covered.**

 This is one of the strongest parts of the current Chapter 4.

 We have:

 - Device: **F-D01–F-D12**
- Edge: **F-E01–F-E15**
- Communication: **F-C01–F-C12**
- Cloud: **F-CL01–F-CL19**
- UI: **F-U01–F-U13**

 This gives us a clear functional decomposition.

 There are also corresponding textual descriptions before each requirement group, which is good because the document is not just a collection of unexplained identifiers.

 **Status: COVERED.**

---

 # 4\. "Is the data well described at every node?"

 ### **Mostly yes, but this deserves one refinement.**

 We have separate sections for:

 - Device data — §4.8
- Device sampling and packet requirements — §4.9
- Device data volume — §4.10
- Edge data — §4.11
- Edge-to-cloud data — §4.12
- Cloud data — §4.13
- UI/API data — §4.14

 That is actually a good response to the official requirement.

 We specify things such as:

 - device identifier
- timestamps
- sequence numbers
- accelerometer
- gyroscope
- latitude/longitude
- position confidence
- proximity
- battery
- device state
- communication state
- event state
- event metadata

 We also specify:

 - approximately 16-byte device identifier
- 64-bit timestamp
- sensor representations
- 32-bit latitude/longitude
- payload limits
- 1-kB edge records
- 1-kB cloud records
- 100-kB UI/API response target

 And we specify candidate formats such as CBOR, Protocol Buffers and JSON.

 ### One thing is still slightly incomplete

 The phrase **"at every node"** could be interpreted as requiring a clearer definition of the data transformation:

 **Sensor → Device data → Edge record → Cloud record → UI/API representation**

 We have these pieces, but they are distributed across several sections.

 I would therefore add a concise data-flow subsection or figure later, rather than substantially changing the requirements.

 **Status: COVERED, with a minor clarity improvement recommended.**

---

 # 5\. "Are all functional specifications well separated from performance specifications?"

 ### **Not completely yet. This is the main issue.**

 We _say_ that they are separated in §4.1.

 We also have functional sections followed by performance sections.

 However, the performance requirements currently have no systematic **P- identifiers**.

 For example:

 > "The device shall provide sensor-acquisition latency of no more than 20 ms..."

 is clearly a performance requirement, but it is not formally identified as something like:

 > **P-D01 — Sensor-acquisition latency: The device shall provide sensor-acquisition latency of no more than 20 ms under nominal operating conditions.**

 Therefore the document currently says:

 **F-requirements are formally identified; performance requirements are mostly embedded in prose.**

 For a document whose official evaluation explicitly asks whether functional and performance specifications are separated, I would fix this.

 ### This is not a conceptual problem.

 The performance content is already there.

 We need to turn it into a formal specification structure.

---

 # 6\. Computational requirements

 The official question asks for:

 > maximum latency, maximum throughput, duty cycle, device-to-edge

 ### Current status: **PARTIALLY COVERED**

 We already have excellent device-side numbers:

 - sensor acquisition ≤20 ms
- preprocessing ≤100 ms
- local event evaluation ≤200 ms
- event decision ≤500 ms
- buffer write ≤100 ms
- duty cycle ≤20%

 We also have device-to-edge application latency ≤2 s.

 ### What is missing?

 The **edge computational performance itself** is not sufficiently explicit.

 For example, we should have measurable targets for:

 - maximum edge processing latency
- edge event-evaluation latency
- edge inference latency
- edge processing throughput
- edge buffering/write performance

 We already have **edge inference ≤200 ms** in the AI section, but it should also be traceable as an edge performance requirement.

 So this area needs a modest expansion.

---

 # 7\. Communications

 Official requirement:

 > wired/wireless, maximum range

 ### **Covered.**

 We explicitly state:

 - device-to-edge = wireless, short-range, low-power, bidirectional
- nominal range ≥10 m
- minimum practical target = 5 m
- application capacity ≥100 kbit/s
- typical latency ≤500 ms
- event delivery ≤2 s
- edge-to-cloud wireless wide-area connectivity
- ≥50 kbit/s/device
- event latency ≤5 s

 This is good.

 The only thing I would eventually formalize is the distinction between:

 **P-Cxx — Communication performance**

 and

 **P-Dxx — Device performance**

 rather than leaving these as prose.

---

 # 8\. Energy

 Official requirement:

 > maximum energy, minimum battery duration, device, edge

 ### **Covered for the device; appropriately qualified for the edge.**

 We have:

 - deep sleep ≤1 mW
- normal monitoring ≤50 mW average
- active sensing ≤150 mW average
- communication burst ≤500 mW peak
- positioning ≤300 mW peak
- minimum battery autonomy 7 days
- engineering objective 14 days

 This is strong.

 For the edge, the document correctly says that the edge is **normally externally powered**.

 That is actually better than inventing an arbitrary battery specification for an edge gateway that may not exist as a dedicated physical device.

 We can formalize this as:

 > Edge energy requirements are deployment-dependent; dedicated portable edge hardware shall receive an energy budget only if such hardware is selected during D3.

 **Status: COVERED.**

---

 # 9\. Mechanical

 Official requirement:

 > maximum size, maximum weight, supports, etc.

 ### **Covered for the device and conditionally covered for the edge.**

 Device:

 - ≤100 cm³
- ≤100 g
- wearable/portable
- −10 °C to +50 °C
- IP65 or better
- 1 m drop resistance

 Dedicated edge:

 - ≤500 g
- ≤2 L
- passive cooling preferred
- continuous operation

 And importantly, the document recognizes that the edge may instead be:

 > smartphone / computer / existing gateway

 So the conditional treatment is technically reasonable.

 **Status: COVERED.**

---

 # 10\. Cloud

 Official requirement:

 > storage size, analytical requirements, UI

 ### **Covered.**

 We have:

 - 100 initial active devices
- scalability objective of 10,000 devices
- ≥100 telemetry messages/s
- ≥20 events/s burst
- API p95 ≤1 s
- cloud event processing p95 ≤2 s
- availability ≥99.5%
- 12-month retention
- 500 GB initial usable application storage
- scalable expansion
- historical queries
- analytics
- AI model management
- APIs
- user/role management
- fleet management

 This is one of the more complete areas.

---

 # 11\. Economic requirements

 ### **Covered.**

 We have:

 - hardware ≤€150/device initial low-volume target
- ≤€100/device larger-scale objective
- recurring communication/cloud ≤€10/device/month
- 100-device first-year operational target ≤€25,000

 And the document explicitly explains what the global target includes and excludes.

 **Status: COVERED.**

---

 # 12\. "Are specifications consistent with the market study?"

 ### **Yes, conceptually.**

 This is actually one of the strengths of the new Chapter 3 → Chapter 4 structure.

 The market study establishes that capabilities such as:

 - location tracking
- geofencing
- notifications
- historical information
- application monitoring

 already exist.

 Chapter 4 consequently does **not** claim those individual functions as novel.

 Instead, the requirements emphasize:

 - distributed processing
- adaptive monitoring
- energy-aware operation
- privacy-aware information flow
- contextual event interpretation
- resilience

 That is logically consistent with Chapter 3.

 The market study → requirements relationship is therefore:

 **Existing capabilities → baseline functions**

 and:

 **identified engineering objectives → additional measurable requirements**

 This is exactly the relationship we want.

---

 # 13\. "Is our IoT design competitive?"

 This needs careful wording.

 ### D2 should **not answer "yes"**.

 And our current Chapter 4 correctly avoids doing so.

 The market study establishes the **baseline and intended differentiation**, but it does not yet establish measured competitiveness.

 To substantiate competitiveness, we would eventually need:

 - implemented SSP
- measured energy consumption
- measured latency
- measured reliability
- measured AI performance
- actual hardware cost
- actual cloud/communication cost
- defined comparison conditions
- comparison with selected competing products

 That belongs naturally in later deliveries.

 So the appropriate D2 statement is:

 > **The market study establishes the existing technological baseline and identifies the engineering dimensions in which SSP is intended to provide integrated capabilities. Commercial competitiveness remains subject to subsequent implementation, measurement and comparative evaluation.**

 That is much more defensible than saying SSP is already competitive.

---

 # 14\. The important conclusion

 I would **not rewrite the whole Chapter 4 from scratch**.

 The technical content is largely there.

 Instead, I recommend one important structural upgrade:

 ### Current structure

 **Functional requirements**

 F-D01...\
 F-E01...\
 F-C01...\
 F-CL01...\
 F-U01...

 ↓

 **Performance specifications expressed mostly as prose**

 Latency...\
 Power...\
 Range...\
 Storage...\
 Cost...

 ### Recommended structure

 **Functional requirements**

 F-D01...F-D12\
 F-E01...F-E15\
 F-C01...F-C12\
 F-CL01...F-CL19\
 F-U01...F-U13

 ↓

 **Performance requirements**

 P-Dxx — Device performance\
 P-Exx — Edge performance\
 P-Cxx — Communication performance\
 P-CLxx — Cloud performance\
 P-Uxx — UI performance\
 P-Sxx — System/end-to-end performance\
 P-AIxx — AI performance\
 P-ECxx — Economic performance

 This would make the answer to the evaluator's question **unambiguous**.

---

 ## 15\. One further improvement I strongly recommend

 I would make **4.1 Specification Principles** explicitly state this relationship:

 > **F- requirements define what SSP shall do. P- requirements define measurable constraints or targets governing how well the corresponding functions shall operate. A single functional requirement may be associated with multiple performance requirements, and a performance requirement may constrain more than one functional requirement.**

 That is a very useful sentence for D2 because it explains why the numbering isn't necessarily one-to-one.

 For example:

 **F-D02 — Position determination**

 can have:

 - **P-D01 — Position update rate**
- **P-D02 — Positioning latency**
- **P-D03 — Positioning energy consumption**
- **P-D04 — Position confidence**

 This is much more engineering-rigorous than trying to force every F into one P.

---

 ## Overall D2 assessment

 | Official question | Current Chapter 4 |
| --- | --- |
| Device functions | **Covered** |
| Edge functions | **Covered** |
| Cloud functions | **Covered** |
| UI functions | **Covered** |
| Data types/formats | **Covered** |
| Data volume/packet size | **Covered** |
| Functional vs. performance separation | **Needs formalization** |
| Device computational performance | **Covered** |
| Edge computational performance | **Needs strengthening** |
| Device-edge communications | **Covered** |
| Energy/device | **Covered** |
| Energy/edge | **Appropriately deployment-dependent** |
| Mechanical/device | **Covered** |
| Mechanical/edge | **Conditionally covered** |
| Cloud/storage/analytics | **Covered** |
| UI performance | **Covered** |
| Economics | **Covered** |
| Consistency with market study | **Covered** |
| Competitiveness | **Correctly deferred to validation** |

### My recommendation

 **Do not submit Chapter 4 exactly as it currently stands.** The issue is not that the requirements are fundamentally missing; it is that the **performance requirements need to be promoted to first-class, uniquely identifiable P-requirements**, particularly for the Device, Edge, Communication, Cloud and UI layers.

 That would turn Chapter 4 from a good collection of specifications into a much more rigorous **requirements specification and traceability framework**, which is particularly appropriate given that the official D2 asks specifically for functional _and performance_ specifications.

 The IEEE formatting guidance itself supports using the appropriate IEEE article structure and template, but the F/P requirement convention is a project-engineering decision rather than an IEEE formatting requirement. ([IEEE Author Center](<https://journals.ieeeauthorcenter.ieee.org/create-your-ieee-journal-article/authoring-tools-and-templates/tools-for-ieee-authors/ieee-article-templates/?utm_source=chatgpt.com>))

 **I would therefore make the next step a systematic conversion of the existing Chapter 4 into F/P requirements, preserving the numerical targets we already established rather than inventing a new set of targets.**
