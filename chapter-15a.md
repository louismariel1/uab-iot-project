The final two chapters are revised below, preserving the original performance and buffering calculations while incorporating both SSP devices, the completed Chapter XII power budgets, satellite connectivity, and the professor's feedback.

The revised structure is:

XV. Performance, Capacity, and Cost Evaluation
XVI. Conclusions and Future Work

Detailed battery calculations remain exclusively in Chapter XII. Chapter XV references their results without duplicating them.

XV. PERFORMANCE, CAPACITY, AND COST EVALUATION
XV.1. Performance Targets

SSP performance is evaluated across the Device, Edge, Cloud, and User Interface layers. The principal requirements defined in TABLE II are:

Wearable: Sensor acquisition ≤20 ms, preprocessing ≤100 ms, and local event decisions ≤500 ms.
Device-to-Edge: BLE event delivery ≤2 s.
Edge: AI inference ≤200 ms and overall processing ≤500 ms.
End-to-end: Normal alert delivery ≤10 s and priority alert delivery ≤5 s under specified terrestrial conditions.
Cloud: API response p95 ≤1 s, event-processing p95 ≤2 s, and service availability ≥99.5%.

End-to-end latency is measured from event detection to presentation in the authorized user interface.

Perimeter-node LoRaWAN latency depends on spreading factor, network loading, and retransmissions. Satellite backhaul introduces additional latency and is not assumed to meet terrestrial alert-delivery targets.

All performance values are design requirements requiring experimental validation.

XV.2. Communication and Processing Capacity

The reference deployment initially targets 100 active devices, with scalability toward 100,000 devices. Cloud capacity targets include 10,000 telemetry messages/s and 300 events/s during bursts.

For N devices transmitting one telemetry message every T seconds:

Rtelemetry=NT

For 100,000 devices reporting every 10 seconds:

Rtelemetry=100,00010=10,000 messages/s

This is a reference capacity scenario. Actual traffic depends on adaptive Wearable reporting and event-driven Perimeter Node communication.

The separate 300 events/s target represents an assumed exceptional-event workload. For example, 3,000 events arriving over 10 seconds require an average processing rate of:

Revents=3,00010=300 events/s

Both workloads may occur simultaneously. The burst rate and duration require validation against representative deployment scenarios.

XV.3. Buffering and Recovery

SSP maintains local monitoring during Cloud connectivity interruptions.

Wearable: Retains selected records within available flash memory.
Perimeter Node: Retains selected event records subject to available storage.
Edge gateway: Targets 24-hour buffering for its assigned devices.
Recovery: Synchronizes queued records after reconnection, prioritizing urgent events.
Reliability: Uses sequence numbers, retries where supported, duplicate suppression, and integrity checks.

Required gateway storage is estimated as:

S=N×R×B×t

where:

N is device count.
R is messages/s/device.
B is stored bytes/message.
t is buffering duration in seconds.

For 100,000 devices, 0.1 messages/s/device, 200 bytes/message, and 86,400 seconds:

S=100,000×0.1×200×86,400
S=172.8 GB

This represents aggregate 24-hour telemetry storage across distributed Edge gateways, excluding metadata, event bursts, filesystem overhead, and safety margins.

Storage allocation must reflect the number of devices assigned to each gateway.

XV.4. Energy and Autonomy Assessment

The complete component-level power budgets are presented in Chapter XII.

SSP Wearable: Section XII.4 evaluates the selected 3.7 V, 500 mAh rechargeable Li-Po battery. The nominal analytical model estimates approximately 21.1 days of autonomy against the 7-day minimum and 14-day engineering objective.
SSP Perimeter Node: Section XII.7.7 evaluates the provisional 3.6 V, 3.6 Ah primary lithium battery, including LoRaWAN spreading factors, GNSS synchronization, regulator efficiency, and self-discharge. The modeled 24-month objective is achievable under reference assumptions, although SF12 provides limited reserve.
Satellite gateway: Chapter X specifies optional satellite backhaul, including terminal power, antenna requirements, and connectivity constraints. Its energy consumption depends on transmission activity and operating mode.

These estimates demonstrate conditional design feasibility, not measured battery autonomy. Prototype testing must verify operating currents, peak loads, duty cycles, battery derating, and environmental effects.

XV.5. Hardware Cost Evaluation

The selected Wearable Configuration A has a preliminary component subtotal of €37.12, as detailed in TABLE XIV.

The Perimeter Node targets a hardware cost of €100–€200 per node. This remains subject to a verified production bill of materials (BOM).

TABLE XV. SSP HARDWARE COST ASSESSMENT

Item	Preliminary value	Status
Wearable components	€37.12	Small-quantity estimate
Wearable retail price	€80–€120	Commercial target
Perimeter Node hardware	€100–€200	Cost target; BOM pending
Edge gateway	Deployment-dependent	Configuration-dependent
Satellite equipment/service	Deployment-dependent	Optional, separate cost

The Perimeter Node BOM must include the MCU, sensors, GNSS, RTC, LoRaWAN radio, antennas, power management, battery, PCB, enclosure, assembly, and testing.

Supplier quotations at 1,000-unit quantities are required to establish production costs. Current estimates do not constitute validated manufacturing prices.

XV.6. Performance and Capacity Verification

Verification shall cover:

Wearable acquisition, preprocessing, and event-detection latency.
BLE and LoRaWAN communication latency and reliability.
Edge AI inference and event-processing latency.
Cloud telemetry throughput and simultaneous event bursts.
API response time, event-processing p95 latency, and availability.
End-to-end alert delivery under terrestrial and satellite connectivity.
CPU, memory, network, and storage utilization.
Gateway buffering, reconnection, and synchronization.
Measured device energy consumption and battery autonomy.
Component compatibility and production BOM verification.

Testing shall assess the initial 100-device deployment and representative scaling scenarios toward 100,000 active devices.

Results must be compared against TABLE II requirements. Analytical estimates, manufacturer specifications, and measured results shall be reported separately.

Tables and Figures Register

Tables

TABLE XV. SSP HARDWARE COST ASSESSMENT.

Figures

No new figures.

Next available identifiers: TABLE XVI and Fig. 15.

XVI. CONCLUSIONS AND FUTURE WORK
XVI.1. Conclusions

This project defines the SmartSecurePerimeter (SSP) IoT architecture, integrating two complementary devices—an SSP Wearable and an SSP Perimeter Node—with distributed Edge processing, Cloud services, and an authorized user interface.

The SSP Wearable combines an nRF52840-based MCU, adaptive IMU and GNSS sensing, BLE communication, tamper detection, haptic feedback, and rechargeable power management. Deterministic event processing remains on the device, while contextual AI inference and predictive geofencing are allocated to the Edge.

The SSP Perimeter Node combines PIR and vibration sensing, LoRaWAN communication, GNSS/RTC synchronization, and low-power primary-battery operation. Shared hardware components simplify integration and support a consistent development platform.

The Edge provides local event correlation, AI inference, buffering, and resilient connectivity. The Cloud supports secure ingestion, historical analytics, multi-device correlation, centralized alert management, and scalable monitoring. Optional satellite backhaul extends gateway connectivity to remote deployments.

The design establishes component selections, implementation alternatives, circuit-level architectures, communication interfaces, data contracts, and quantitative performance estimates.

Analytical power budgets indicate potential compliance with the Wearable's 7–14-day and Perimeter Node's 12–24-month autonomy objectives under stated assumptions. Performance and capacity calculations support preliminary engineering feasibility but do not constitute experimental validation.

Overall, the proposed SSP architecture provides a technically structured basis for prototype integration, testing, and subsequent system development.

XVI.2. Future Work

The next development phase will prioritize:

Hardware validation: PCB integration, electrical compatibility, sensor interfaces, peak-current measurements, and environmental testing.
Energy validation: Measured Wearable and Perimeter Node power budgets, adaptive duty-cycle optimization, and battery-autonomy testing.
Communication testing: BLE, LoRaWAN, terrestrial backhaul, and optional satellite connectivity.
Performance verification: Device and Edge latency, Cloud throughput, event-burst processing, and 24-hour buffering.
Security and reliability: Authentication, encryption, recovery, synchronization, and fault handling.
Cost validation: Complete BOM, 1,000-unit supplier quotations, assembly estimates, and production feasibility.

These activities will establish measured compliance with the SSP functional, performance, energy, and cost requirements.

Tables and Figures Register

Tables: None.

Figures: None.

Final numbering: TABLE XV and Fig. 14 are the last tables and figures used in the revised report.

Final D4 Consistency Checkpoint

Chapters XII–XVI

Revised

Final table: TABLE XV

Final figure: Fig. 14

Assumes no additional tables or figures are introduced in the References or Annexes.

The revised chapters now have distinct responsibilities: Chapter XII contains both device power budgets; Chapter XIII justifies implementation choices; Chapter XIV defines communication data contracts; Chapter XV evaluates system performance, capacity, and cost; and Chapter XVI summarizes the design and outstanding validation work.

One important limitation remains: the professor's request for verified component prices at 1,000-unit quantities and a complete stationary-node production BOM is not yet fully satisfied. These should be explicitly tracked during the final feedback-compliance audit, together with the satellite peak-power and communication-timing evidence.

The main report chapters are now ready for that final audit and a cross-reference check against the References and Annexes.
