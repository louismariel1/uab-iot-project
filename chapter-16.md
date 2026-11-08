# XVI. PERFORMANCE AND CAPACITY ESTIMATION

## XVI.1. Performance Targets

SSP performance is evaluated across wearable processing, device-to-edge communication, edge AI inference, cloud processing, and end-to-end alert delivery.

The principal targets defined in Table 2 include:

- **Wearable:** Sensor acquisition ≤20 ms, local preprocessing ≤100 ms, and local event decisions ≤500 ms.
- **Device-to-edge:** BLE event delivery ≤2 s.
- **Edge:** AI inference ≤200 ms and overall edge processing ≤500 ms.
- **End-to-end:** Normal alert delivery ≤10 s and priority alert delivery ≤5 s.
- **Cloud:** API response p95 ≤1 s, event-processing p95 ≤2 s, and service availability ≥99.5%.

End-to-end latency is measured from the sensor-event timestamp to presentation in the authorized user interface. These targets are evaluated under representative operating and connectivity conditions.

## XVI.2. Communication and Processing Capacity

The cloud architecture supports the following capacity targets:

- **Initial deployment:** At least 100 active devices.
- **Telemetry ingestion:** At least 100 messages/s.
- **Event processing:** At least 20 events/s during bursts.
- **Scalability:** Expansion toward 10,000 active devices.

The required telemetry ingestion rate can be estimated as:

$$\
R\_{\mathrm{telemetry}}=\frac{N}{T}\
$$

where $N$ is the number of active devices and $T$ is the average telemetry transmission interval in seconds, assuming one message per device per interval.

For example, 100 devices transmitting every 10 seconds generate approximately 10 messages/s. At 10,000 devices, the same interval generates approximately 1,000 messages/s.

These examples illustrate the relationship between deployment size and communication capacity; the actual transmission interval depends on the adaptive monitoring configuration.

## XVI.3. Buffering and Recovery

SSP maintains locally supported monitoring during cloud connectivity interruptions.

- **Wearable:** Buffers selected events and telemetry within available local memory.
- **Edge gateway:** Supports the specified 24-hour buffering target.
- **Recovery:** Synchronizes queued records after reconnection, prioritizing urgent events.
- **Reliability:** Uses retries, sequence numbers, duplicate suppression, and data-integrity checks to support reliable delivery.

The required gateway storage capacity depends on message size, transmission frequency, device count, and the buffering period.

A simplified estimate is:

$$\
S=N\times R\times B\times t\
$$

where $N$ is the number of devices, $R$ is the average message rate per device, $B$ is the average stored message size in bytes, and $t$ is the buffering duration in seconds.

Storage overhead, event bursts, metadata, and safety margins must also be considered.

## XVI.4. Capacity Estimation and Verification

Performance and capacity are verified through representative integration, load, and recovery testing.

The principal measurements include:

- Wearable processing latency and BLE event-delivery time.
- Edge AI inference and event-processing latency.
- Cloud telemetry throughput and event-burst handling.
- API and event-processing p95 latency.
- End-to-end alert-delivery time.
- CPU, memory, network, and storage utilization.
- Buffering capacity, reconnection, and data synchronization.
- Availability and scalability under increasing device loads.

Testing shall assess both the initial 100-device deployment and representative scaling scenarios toward 10,000 devices. Results are compared with the requirements in Table 2.

# XVII. CONCLUSIONS

This project defines the SmartSecure-Perimeter (SSP) IoT architecture, integrating a low-power wearable, edge gateway, cloud back-end, and user interface. It establishes the distribution of sensing, deterministic event detection, AI-based risk assessment, communication, storage, and monitoring functions.

The wearable integrates an nRF52840 microcontroller, adaptive IMU and GNSS sensing, BLE communication, tamper detection, haptic feedback, and rechargeable power management. Contextual AI inference and predictive geofencing are performed at the Edge, while the Cloud supports historical analytics, multi-device correlation, and centralized services.

The proposed design targets a minimum seven-day battery autonomy, with a fourteen-day engineering objective, and supports local processing and buffering during connectivity interruptions. The implementation options, component selections, circuit architecture, energy model, data contracts, and performance targets provide a technical basis for system integration.

Component-level power estimates, hardware integration, communication reliability, and performance and capacity targets require verification through prototype implementation and testing.

### Final consistency review

The revised closing chapters now align with the rest of D4:

- Chapter XVI: Preserves the original performance targets and adds explicit formulas for telemetry throughput and gateway buffering capacity.
- Chapter XVII: Removes both obsolete SSP configurations and the reference to D3 as the current milestone.
- Architecture: Maintains deterministic wearable processing, Edge AI for contextual inference and predictive geofencing, and Cloud AI for historical analytics.
- Requirements: Retains the 7-day minimum and 14-day battery objective, 24-hour gateway buffering, and the performance and scalability targets from Table 2.

Status: Chapters XVI and XVII are ready for integration into the D4 report.

Understood. The professor's instruction is to present the intended system capacity of 100,000 devices as the primary performance requirement, rather than emphasizing an initial deployment of 100 devices.

I agree. For D4, we should remove the 100-device deployment baseline from the performance specification and consistently use 100,000 active devices as the scalability target.

### Revised Section XVI.2

## XVI.2. Communication and Processing Capacity

SSP targets support for **100,000 active wearable devices** through a distributed architecture with multiple edge gateways and horizontally scalable cloud services.

The required telemetry ingestion rate is estimated as:

$$\
R\_{\mathrm{telemetry}}=\frac{N}{T}\
$$

where $N$ is the number of active devices and $T$ is the average telemetry transmission interval in seconds.

For 100,000 devices transmitting one message every 10 seconds:

$$\
R\_{\mathrm{telemetry}}=\frac{100,000}{10}\
\=10,000\ \mathrm{messages/s}\
$$

The cloud architecture therefore targets at least **10,000 telemetry messages/s** under this operating assumption.

Scalability is supported through distributed edge processing, multiple gateways, scalable message ingestion, and independently scalable cloud processing and storage. Actual capacity depends on message frequency, payload size, event bursts, and available infrastructure resources.

The 100,000-device capacity and associated throughput are design targets to be verified through load and scalability testing.

### Required consistency updates

The following changes should also be made elsewhere in the D4 report:

| Location                              | Updated requirement                                  |
| ------------------------------------- | ---------------------------------------------------- |
| Chapter V — Table 2                   | 100,000 active devices                               |
| Chapter V — Table 2                   | ≥10,000 telemetry messages/s at a 10-second interval |
| Chapter XIV.3 — Cloud Back-End        | Target 100,000 devices instead of 100/10,000         |
| Chapter XVI.4 — Capacity Verification | Test scalability against the 100,000-device target   |
| Chapter XVII — Conclusions            | Reference scalability toward 100,000 devices         |

One additional point: The existing 20 events/s target must also be revised or explicitly scoped. Otherwise, it would be inconsistent with a system designed for 100,000 devices. Event capacity should be derived from an assumed event-generation rate and burst factor, rather than assigning an unsupported number.

This approach addresses the professor's feedback directly: the D4 report specifies what SSP is designed to support, not merely how many devices an initial prototype deployment might contain.
