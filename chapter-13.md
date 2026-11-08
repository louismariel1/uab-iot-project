# XIII. WEARABLE HARDWARE DESIGN AND CIRCUIT-LEVEL IMPLEMENTATION

## XIII.1. Design Overview

The SSP wearable is a low-power, self-contained device for motion, positioning, and tamper monitoring, with Bluetooth Low Energy (BLE) communication and haptic feedback. The wearable performs deterministic local event processing, while contextual inference and risk prediction are executed at the Edge and Cloud layers.

The hardware integrates a low-power microcontroller, adaptive sensors, power-management circuitry, a rechargeable battery, communication interfaces, and a haptic actuator. The design follows the functional, physical, environmental, energy, and cost requirements specified in Table 2.

The wearable targets a maximum volume of 100 cm³, mass of 100 g, IP65 ingress protection, and resistance to a drop of at least 1 m. The enclosure and skin-contact materials shall tolerate perspiration, rain, cleaning, and intended disinfection while supporting tamper-resistant construction.

## XIII.2. System Architecture

Figure 8 presents the complete wearable electronic architecture, integrating power management, the microcontroller, adaptive sensors, communication interfaces, tamper detection, and haptic feedback. The nRF52840 microcontroller coordinates motion sensing, GNSS positioning, local event processing, and BLE communication with the edge gateway. The BQ25120A power-management circuit supplies the electronic subsystems, while adaptive sensor operation and controlled actuator activation support energy-efficient monitoring.

**Figure 8: Complete wearable electronic architecture.**

## XIII.3. MCU and Sensor Interconnections

Figure 9 presents the principal interfaces between the nRF52840 microcontroller, BMI270 inertial measurement unit (IMU), MAX-M10S GNSS receiver, DRV5032 tamper sensor, and haptic actuator. The IMU communicates through I²C and interrupt lines, the GNSS receiver through UART, and the tamper sensor through a digital GPIO input. The MCU controls haptic activation through an N-MOSFET switching driver and exchanges telemetry with the edge gateway using integrated BLE.

The diagram represents functional signal connections. The GNSS supply and I/O levels must match the selected logic domain, while the haptic driver must accommodate the motor's operating voltage and current.

**Figure 9: MCU and sensor interconnection diagram.**

## XIII.4. Power-Management Circuit and Energy Budget

Figure 10 illustrates the wearable power architecture, including USB-C input protection, the BQ25120A power-management integrated circuit, and a rechargeable 3.7 V, 500 mAh Li-Po battery with protection and temperature monitoring. The PMIC manages charging and provides a regulated 1.8 V supply for compatible electronic components. The haptic motor is controlled through an N-MOSFET driver and requires a suitable supply arrangement.

The wearable reduces energy consumption through low-power MCU states, adaptive IMU sampling, intermittent GNSS positioning, event-driven BLE transmission, local event filtering, and controlled haptic activation.

**Figure 10: Power-management circuit (charging, regulation, and loads).**

### XIII.4.1. Operating Profile and Assumptions

The nominal energy model uses the operating-state allocations defined in Table 3: at least 95% minimum activity, up to 4% sensing and local processing, and up to 1% wireless communication bursts.

GNSS operation is initially modelled with a 1% active duty cycle. Exceptional events, including increased sensing, additional communication, and haptic activation, are considered separately.

The battery calculation assumes a nominal voltage of 3.7 V and an 80% usable-energy fraction.

### XIII.4.2. Component-Level Power Budget

Average power consumption is estimated using:

$$\
P\_{\mathrm{avg}}=\sum\_{i=1}^{n}P_i d_i\
$$

where $P_i$ represents component power in operating state $i$ and $d_i$ is its operating-time fraction.

**Table XIII-I: Preliminary Average Power Budget**

| Component                               | Assumed Average Power |
| --------------------------------------- | --------------------- |
| MCU and processing                      | 0.50 mW               |
| IMU                                     | 0.57 mW               |
| GNSS (135 mW active, 1% duty cycle)     | 1.35 mW               |
| BLE communication                       | 0.15 mW               |
| Local memory                            | 0.05 mW               |
| Power management and battery monitoring | 0.30 mW               |
| **Total**                               | **2.92 mW**           |

The values are retained from the original D3 energy model as an illustrative nominal operating scenario. The selected component operating currents, regulator losses, GNSS acquisition behaviour, and exceptional-event loads determine the actual power budget.

### XIII.4.3. Battery Capacity and Autonomy

Required nominal battery capacity is estimated as:

$$\
C\_{\mathrm{req}}=\
\frac{P\_{\mathrm{avg}}\times t}\
{V\_{\mathrm{bat}}\times\eta}\
$$

where $C\_{\mathrm{req}}$ is in Ah, $P\_{\mathrm{avg}}$ in W, $t$ in hours, $V\_{\mathrm{bat}}$ in volts, and $\eta$ is the usable-energy fraction.

**Table XIII-II: Estimated Battery Capacity Requirements**

| Operating Duration | Required Capacity |
| ------------------ | ----------------- |
| 7 days             | 166 mAh           |
| 14 days            | 331 mAh           |

For the selected 500 mAh battery:

$$\
E\_{\mathrm{usable}}=3.7\times0.5\times0.8=1.48\ \mathrm{Wh}\
$$

At the assumed average consumption of 2.92 mW:

$$\
t=\frac{1.48}{0.00292}\
\approx507\ \mathrm{h}\
\approx21.1\ \mathrm{days}\
$$

The corresponding maximum average-power budgets are approximately **8.81 mW for seven days** and **4.40 mW for fourteen days**. These values provide the energy-design limits under the stated battery assumptions.

## XIII.5. PCB and Component Integration

Figure 11 illustrates the proposed wearable printed circuit board (PCB), including the main electronic components, GNSS antenna connection, haptic driver, and battery integration. The indicative 38 × 38 mm PCB arrangement considers signal routing, power distribution, sensor placement, and antenna clearance.

The side-view stack-up illustrates the PCB, rechargeable battery, and enclosure, with an approximate thickness of 11 mm as the preliminary mechanical design target. The component-zoning view separates power management, sensing, processing, positioning, tamper detection, and haptic actuation.

The enclosure design incorporates the charging interface, mechanical fastening, sealing, and materials required for wearability and environmental protection.

**Figure 11: PCB and component integration (indicative layout and dimensions).**

## XIII.6. Component Summary

Table XIII-III summarizes the selected wearable electronic components. Their alternatives, selection rationale, and indicative costs are presented in Chapter XIV.

**Table XIII-III: Main Components (SSP Wearable)**

| Ref. | Component (Model)              | Function / Key Specification                            |
| ---- | ------------------------------ | ------------------------------------------------------- |
| U1   | TI BQ25120A                    | Li-Po charging, power-path management, 1.8 V regulation |
| U2   | Raytac MDBT50Q-1MV2 (nRF52840) | MCU with BLE, 1 MB flash and 256 KB RAM                 |
| U3   | Bosch BMI270                   | Six-axis IMU, adaptive motion sensing                   |
| U4   | u-blox MAX-M10S                | GNSS receiver, adaptive positioning                     |
| U5   | TI DRV5032                     | Magnetic tamper detection                               |
| Q1   | N-MOSFET                       | Haptic motor switching                                  |
| M1   | ERM vibration motor            | Local haptic warning                                    |
| BAT  | 3.7 V, 500 mAh protected Li-Po | Rechargeable battery with NTC                           |
| ANT  | GNSS antenna                   | GNSS signal reception                                   |

Additional passive components, protection circuitry, connectors, and PCB manufacturing elements are included in the detailed bill of materials.

## XIII.7. Key Design Outcomes and Verification

The proposed wearable design combines adaptive sensing, local processing, BLE communication, tamper detection, and haptic feedback within the specified physical and energy constraints.

The principal design outcomes are:

1. Integrated BQ25120A power management with a regulated 1.8 V logic supply.
2. nRF52840 MCU with integrated BLE and deterministic event processing.
3. Adaptive BMI270 motion sensing and MAX-M10S GNSS positioning.
4. Magnetic tamper detection and MCU-controlled haptic feedback.
5. Indicative PCB dimensions of 38 × 38 mm and approximately 11 mm stack-up thickness.
6. Minimum seven-day battery-autonomy requirement and fourteen-day engineering objective.

Hardware verification covers component electrical compatibility, power consumption, battery autonomy, sensing and event-processing latency, BLE connectivity, local buffering, tamper detection, and haptic operation. Physical testing addresses mass, volume, operating temperature, ingress protection, drop resistance, and skin-contact material suitability.

The detailed comparison of component alternatives, selected technologies, and implementation costs is presented in Chapter XIV.

### Changes relative to your current Chapter XIII

The original seven subsections, hardware selections, Figures 8–11, and technical descriptions have been preserved. I made four focused additions:

1. Restored physical, environmental, and wearability requirements in XIII.1.
2. Expanded XIII.4 with the original energy assumptions, power budget, battery-capacity calculations, and autonomy estimates.
3. Added a concise hardware-verification paragraph to XIII.7 instead of creating an eighth subsection.
4. Renumbered the tables sequentially as XIII-I, XIII-II, and XIII-III.

One important technical distinction: The 2.92 mW estimate and 21.1-day autonomy are inherited modelling assumptions, not measured values for the selected components. The 7-day and 14-day power limits are more useful as design constraints.

Recommendation: Adopt this as the updated Chapter XIII. It restores the important material from D3 without unnecessarily expanding the report or duplicating the implementation comparisons planned for Chapter XIV.
