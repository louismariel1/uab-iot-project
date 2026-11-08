I agree with your proposed sequence. It is a sound way to approach D4 because it separates updating the report structure, developing the detailed hardware design, removing the obsolete product variant, and making the final implementation selections.

I would make one important distinction: we should preserve the existing D3 report as the baseline and evolve it into the D4 report, rather than reorganising or rewriting it unnecessarily. That will maintain continuity with the work already submitted and make the D4 changes traceable.

I have located and retrieved the current `Group14_SSP_P3.pdf` (the 19-page version uploaded on 8 November). Its existing structure already contains a chapter titled XIV. Wearable Circuit-Level Design. This is useful: we should extend and substantially develop that chapter, not introduce a disconnected hardware-design chapter elsewhere.

## 1. Current D3 report structure

The PDF has the following main structure:

| Section    | Existing chapter                               |
| ---------- | ---------------------------------------------- |
| I          | Introduction                                   |
| II         | System Concept and Architecture                |
| III        | Operational Storyboard                         |
| IV         | Market Benchmark and Economic Target           |
| V          | Functional and Performance Specification       |
| VI         | Distributed AI Strategy and Energy Model       |
| VII        | Security, Privacy, and Physical Design         |
| VIII       | Validation Approach                            |
| IX         | Global End-to-End IoT Architecture             |
| X          | Communication Architecture                     |
| XI         | Edge Software Architecture                     |
| XII        | Cloud Back-End and UI Front-End Architecture   |
| XIII       | Implementation Options and Selection Rationale |
| XIV        | Wearable Circuit-Level Design                  |
| XV         | Data Contracts, Payloads and APIs              |
| XVI        | Performance and Capacity Estimation            |
| XVII       | Conclusions                                    |
| Appendix A | Detailed D2 Requirement Matrix                 |

The existing Chapter XIII already has:

- XIII.1 Wearable Hardware
- XIII.2 Edge Gateway Hardware and Connectivity
- XIII.3 Cloud Back-End Technologies
- XIII.4 User Interface and API Technologies
- XIII.5 Selected Baseline and Validation

The existing Chapter XIV has:

- XIV.1 Design Requirements and Assumptions
- XIV.2 Proposed Electronic Circuit Architecture
- XIV.3 Battery Technology and Selection
- XIV.4 Power Budget and Battery Autonomy Estimation
  - XIV.4.1 Assumptions and Operating Profile
  - XIV.4.2 Component-Level Power Budget
  - XIV.4.3 Battery Capacity and Autonomy Estimation
- XIV.5 Energy-Saving Design Measures
- XIV.6 Preliminary Design Validation

This means we already have a good foundation. However, the current Chapter XIV is still preliminary: it describes functional blocks and a proposed circuit architecture, but does not yet provide the component-level engineering detail expected from the lecturer.

## 2. Proposed updated Chapter XIV

I recommend extending Chapter XIV while retaining its existing numbering and relevant material.

Proposed title: XIV. Wearable Hardware Design and Circuit-Level Implementation

| Subsection | Proposed content                                       |
| ---------- | ------------------------------------------------------ |
| XIV.1      | Design Requirements, Constraints and Assumptions       |
| XIV.2      | Wearable Hardware Architecture and Functional Blocks   |
| XIV.3      | Component Options and Technical Comparison             |
| XIV.4      | Selected Hardware Components and Selection Rationale   |
| XIV.5      | Detailed Electronic Circuit and Interconnection Design |
| XIV.6      | Power Management, Battery Charging and Protection      |
| XIV.7      | PCB Design, Interfaces and Physical Integration        |
| XIV.8      | Component-Level Power Budget and Battery Autonomy      |
| XIV.9      | Preliminary BOM and Hardware Cost Estimation           |
| XIV.10     | Hardware Verification and Performance Validation       |

This gives us a logical progression:

1. Establish what the wearable must achieve.
2. Define its hardware architecture.
3. Compare real market-available components.
4. Select the preferred components and justify the decisions.
5. Show exactly how the components connect electrically.
6. Explain the power architecture.
7. Address PCB, antenna, enclosure and physical constraints.
8. Calculate power consumption and autonomy.
9. Estimate hardware costs.
10. Define how the design will be verified.

One important point: the component comparison and selection should be based on actual manufacturer datasheets, exact part numbers, electrical compatibility and indicative prices. We should not simply list component families such as Nordic, ESP32 or STM32.

### Circuit diagrams to develop

[NRF52832 Schematic Review - Nordic Q&A - Nordic DevZone - Nordic DevZone](https://images.openai.com/static-rsc-4/apgPQ7V6yPpdTdvAhJy-jNQAaedQkPp5j3ByvQseArV_jJ0yicaDKxfNqfOsUdnvVjMVgwyy_zHJCCAkZwu18sScrLri1jt8rS1hC7a5iniXgXpfPyfL2n7PlHz6jqgZakSmPKT8bpCC-QivFXRD4RsXtKqXY2Qv1SIZp30tOgw?purpose=inline)

[STEVAL-STRKT01 (#1): LoRa® (LoRaWAN™) GNSS (GPS) Asset Tracker/Data Logger](https://images.openai.com/static-rsc-4/1u9F_g2XNx_YxkT_SMcLysuIvRfQ3jEbEkI2HadR46xoaq95rUXp2STezVqqKtvwytHosOnbF2YU88C1avsZy4vVJYFAoikhMUNXHsHnsrZ0UqO3lt5FFT5QS3q-89uHMOKFCSM52NcuwKZrjpcmmn9X1srRAMUZU-B6IFGtMQc?purpose=inline)

[Scheda pcb per monitoraggio salute indossabile, tracker fitness con sensori esp32, firmware](https://images.openai.com/static-rsc-4/xZgZ8XHEvulM7kjj6H08zsiwZZ9-sRzsUaJbIi8OdXiDZ7bVVP6QAVUihEJrvkpVzN1TQ8oocK1l58OW1JCmg5uuD0-AocGExllSHepddkeYwcxqc2hM7Mm44qZ1h6riQLwUsaG05sM_TmiXLKhvbInPSkHpvXcNoYDR3vkqilk?purpose=inline)

12

I suggest developing at least these diagrams:

- Figure 8 — Complete wearable electronic architecture: all components, power rails and interfaces.
- Figure 9 — MCU and sensor interconnection schematic: MCU, IMU, GNSS, tamper sensors, memory and communication interfaces.
- Figure 10 — Power-management circuit: battery, charging, protection, regulators, voltage monitoring and power switches.
- Figure 11 — Wearable PCB/component integration: indicative physical arrangement, antenna considerations and connectors.

These should be engineering diagrams based on the components we actually compare and select, rather than illustrative block diagrams.

## 3. Remove the AI-Wearable configuration

I agree that we should remove the second configuration throughout the report.

The resulting product architecture will be:

## SSP Standard — Single Product Architecture

Device — Wearable

Sensors, deterministic local processing, BLE, temporary storage, tamper detection and haptic feedback.

BLE

Edge — Gateway

Sensor fusion, contextual risk assessment, trajectory prediction, geofencing and Edge AI.

MQTT over TLS / HTTPS

Cloud — Back-end

Persistent storage, historical analysis, multi-device correlation, Cloud AI and alert services.

Authorized access

User Interface

Operator monitoring, alerts, historical reports and administration.

The wearable remains capable of deterministic local event detection. AI inference is assigned to Edge and Cloud.

We should also review the physical sensor requirements. For example, tamper detection should be supported by an appropriate physical sensor, such as a magnetic/Hall-effect sensor or mechanical switch, rather than relying exclusively on an AI function.

The removal must cover:

- Executive Summary and Introduction.
- System Concept and Architecture.
- Operational Storyboard, where applicable.
- Market Benchmark and Economic Target.
- Functional and Performance Specification.
- Distributed AI Strategy and Energy Model.
- Implementation Options and Selection Rationale.
- Wearable Circuit-Level Design.
- Battery and power calculations.
- Validation Approach.
- Conclusions.
- Appendix A requirement matrix.

We must also remove obsolete AI-Wearable-specific RAM, battery, power-budget and price assumptions. Those values should not simply be transferred to SSP Standard.

## 4. Ensure options are available at every architecture layer

Your fifth point is particularly important. The existing Chapter XIII already contains options for all the major layers, but we need to ensure that each comparison is sufficiently concrete and that the final selections are supported.

I suggest the following review:

| Layer  | Existing options to develop further                                                               |
| ------ | ------------------------------------------------------------------------------------------------- |
| Device | MCU/SoC, IMU, GNSS, tamper sensors, memory, BLE, battery, charging, regulation, haptic actuator   |
| Edge   | ARM platform, processing, AI execution, storage, Ethernet/Wi-Fi/cellular connectivity             |
| Cloud  | Cloud provider, MQTT ingestion, databases, analytics, AI services, identity and access management |
| UI     | Web framework, mobile framework, APIs, real-time notifications and visualisation                  |

For each layer, we should distinguish:

- Options: technically viable alternatives.
- Preferred candidate: the option currently favoured.
- Final selection: the component or technology adopted for D4.
- Rationale: why it is preferred against the requirements.
- Evidence: datasheets, technical specifications, prices and calculations.

This avoids presenting an early preference as though it were already a fully justified final selection.

## 5. D4 implementation selection

Once the hardware design and options have been developed, we can update Chapter XIII.5 and Chapter XIV to document the final implementation baseline.

For the Device layer, this means going beyond selecting an MCU and an IMU. The selection must include the supporting circuit elements:

- MCU/SoC and BLE radio.
- IMU and GNSS.
- Tamper detection sensors.
- Local memory, if required.
- Haptic actuator and driver.
- Battery and charging/protection circuit.
- Voltage regulators and power-management components.
- Antenna, programming/debug interface and supporting passive components.

The final schematic and component list must be electrically consistent. For example, the selected MCU must support the interfaces required by the chosen sensors, and the voltage rails must satisfy all connected components.

For Edge and Cloud, we should likewise move from general technology options to justified D4 selections.

## 6. D4 presentation

The presentation should follow the same engineering logic as the report, but with less detail.

I would organise the D4 slides around:

1. D4 objective and implementation approach.
2. Complete SSP Standard architecture.
3. Wearable hardware architecture.
4. Component options and comparison.
5. Selected wearable components and rationale.
6. Wearable circuit-level schematic.
7. Power architecture and battery autonomy.
8. Edge hardware and software selection.
9. Cloud and UI implementation selection.
10. Performance, cost and requirement compliance estimates.
11. Prototype progress and validation evidence.
12. Conclusions and remaining implementation work.

We can adjust the slide count to the official presentation requirements, but this gives us a useful starting structure.

## 7. Recommended execution order

I would follow your proposed sequence, with one small refinement: agree on the updated table of contents before writing the new chapter.

1. Freeze the existing D3 structure as our baseline.

   Record the current headings and identify which sections need modification.
2. Approve the extended Chapter XIV structure.

   Add the hardware-design subsections while preserving the rest of the report.
3. Develop and complete Chapter XIV.

   Research components, compare options, create circuit diagrams, calculate power and battery requirements, and establish the hardware BOM.
4. Integrate the chapter into the report.

   Check figure numbering, tables, cross-references and consistency with existing sections.
5. Remove the AI-Wearable variant throughout.

   Update all descriptions, requirements, tables, calculations, diagrams and conclusions.
6. Review Device, Edge, Cloud and UI options.

   Ensure the alternatives and selection rationales are sufficiently clear at every layer.
7. Complete the D4 implementation baseline.

   Update the preferred selections, technical justifications, circuit elements, cost and performance estimates.
8. Update the D4 slides.

   Align them with the final report and the lecturer's feedback.

My recommendation: let's start with Step 1 and Step 2 only. I suggest we first agree on the revised table of contents, including the proposed Chapter XIV subsections, before doing component research or drafting circuit diagrams. That gives us a stable structure and prevents unnecessary rewriting later.
