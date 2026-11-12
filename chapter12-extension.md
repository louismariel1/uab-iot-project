Yes. The stationary-node power budget and 12–24-month battery-autonomy justification are explicit parts of the professor's feedback.

I recommend adding a dedicated subsection within XII.7 — SSP Perimeter Node Hardware, immediately after the low-power operating strategy.

The revised structure will be:

- XII.7.6. Low-Power Operating Strategy
- XII.7.7. Component-Level Power Budget and 12–24-Month Battery Autonomy — new quantitative section
- XII.7.8. Physical Integration

This keeps the Wearable power budget in XII.4 and the Perimeter Node power budget in XII.7, with no duplicated derivations in Chapter XV.

The following section is ready to insert into Chapter XII.

### XII.7.7. Component-Level Power Budget and 12–24-Month Battery Autonomy

The SSP Perimeter Node uses a provisional **3.6 V, 3.6 Ah primary lithium battery**, targeting a minimum autonomy of 12 months and an extended objective of 24 months. The power budget accounts for background operation, LoRaWAN transmission, GNSS synchronization, event processing, conversion losses, and battery self-discharge.

#### A. Reference Operating Profile

**TABLE IX. SSP PERIMETER NODE POWER-BUDGET ASSUMPTIONS**

| Component / Operation           | Reference assumption               |
| ------------------------------- | ---------------------------------- |
| Background electronics          | 24 µA at 3.3 V, continuous         |
| LoRaWAN transmission            | 119 mA at 3.3 V                    |
| LoRaWAN reception               | 5 mA at 3.3 V, 200 ms/uplink       |
| Radio traffic                   | 24 uplinks/day                     |
| GNSS synchronization            | 13.8 mA at 3.0 V, 240 s/day        |
| Event processing                | Additional 5 mA at 3.3 V, 10 s/day |
| Converter efficiency            | 90% assumed                        |
| Regulator quiescent current     | 360 nA at 3.6 V                    |
| Initial usable battery capacity | 70%                                |
| Battery self-discharge          | 2% per month                       |

The background-current allowance represents the combined low-power electronics, including the MCU, sensors, RTC, and sleeping radio. Active radio and GNSS loads are evaluated separately. These assumptions require component-level measurement and verification.

#### B. Daily Energy Consumption

For each operating state, energy is estimated as:

[\
E_i=\frac{V_i I_i t_i}{3600}\
]

where (E_i) is energy in Wh, (V_i) is voltage in V, (I_i) is current in A, and (t_i) is operating time in seconds.

The total daily battery energy is approximated by:

[\
E\_{\mathrm{bat,day}}=\
\frac{\sum E_i}{\eta}\
+V\_{\mathrm{bat}}I_q(24)\
]

where (\eta=0.90) is the assumed converter efficiency and (I_q=360) nA is the regulator quiescent current. The model treats conversion efficiency as constant for preliminary estimation.

LoRaWAN airtime is evaluated for a 20-byte physical-layer payload, 125 kHz bandwidth, coding rate 4/5, eight-symbol preamble, explicit header, and CRC.

**TABLE X. SSP PERIMETER NODE LORAWAN ENERGY AND AUTONOMY**

| Parameter                         | SF7    | SF10    | SF12      |
| --------------------------------- | ------ | ------- | --------- |
| Airtime/uplink (ms)               | 56.576 | 370.688 | 1,318.912 |
| Regulated energy (mWh/day)        | 4.877  | 5.699   | 8.182     |
| Battery energy (Wh/year)          | 1.989  | 2.323   | 3.330     |
| Required capacity (Ah, 24 months) | 2.052  | 2.396   | 3.435     |

Increasing the spreading factor increases transmission airtime and energy consumption. Reception is represented by a simplified allowance; complete LoRaWAN Class A receive windows, retransmissions, and network overhead require validation.

#### C. Battery Capacity and Self-Discharge

Nominal battery energy is:

[\
E\_{\mathrm{nominal}}=3.6\times3.6\
\=12.96\ \mathrm{Wh}\
]

Assuming 70% initially usable energy:

[\
E_0=12.96\times0.70\
\=9.072\ \mathrm{Wh}\
]

With an assumed monthly self-discharge rate of 2%, the remaining energy is estimated recursively:

[\
E\_{m+1}=0.98E_m-\frac{E\_{\mathrm{bat,year}}}{12}\
]

where (E_m) is remaining battery energy after month (m).

After 24 months, the estimated remaining energy is:

- **SF7:** 2.402 Wh.
- **SF10:** 1.868 Wh.
- **SF12:** 0.256 Wh.

The reference 3.6 Ah battery therefore satisfies the modeled 24-month objective under all three baseline spreading-factor scenarios. However, SF12 has limited reserve and is sensitive to additional transmissions, GNSS activity, temperature, and battery ageing.

#### D. Sensitivity and Design Constraints

The extended autonomy objective depends on maintaining the assumed operating profile.

At SF12, increasing regulated consumption by 1 mWh/day raises the estimated required battery capacity to approximately 3.85 Ah, exceeding the 3.6 Ah baseline. Doubling daily GNSS synchronization activity to 480 seconds increases the requirement to approximately 4.59 Ah.

The power architecture must also support radio transmission peaks independently of average energy consumption. Regulator efficiency, voltage compatibility, battery pulse capability, and environmental derating require hardware validation.

A solar-assisted alternative would require a rechargeable battery and dedicated charging circuitry; the selected primary lithium battery must not be recharged.

#### E. Engineering Assessment

The analytical results indicate that the selected battery can support the **12-month minimum** and potentially the **24-month extended objective**, provided the reference duty cycle is maintained.

The 24-month SF12 result is marginal. Final battery selection requires measured operating currents, complete LoRaWAN transaction profiling, GNSS synchronization measurements, battery discharge characteristics, and environmental testing.

The calculations are design estimates, not experimentally demonstrated autonomy.

## Updated Chapter XII tables and figures register

Because this section is inserted into Chapter XII, its two tables must appear before the tables currently numbered in Chapter XIII.

| Chapter XII table | Description                                    |
| ----------------- | ---------------------------------------------- |
| TABLE VI          | Wearable component-level power budget          |
| TABLE VII         | Wearable battery capacity and autonomy         |
| TABLE VIII        | Wearable component summary                     |
| TABLE IX          | SSP Perimeter Node Power-Budget Assumptions    |
| TABLE X           | SSP Perimeter Node LoRaWAN Energy and Autonomy |

Chapter XII figures remain unchanged: Figs. 10–14.

The subsequent tables must be renumbered:

| Chapter XIII table                     | New identifier |
| -------------------------------------- | -------------- |
| Configuration A — Selected Wearable    | TABLE XI       |
| Configuration B — Alternative Wearable | TABLE XII      |
| Configuration C — Alternative Wearable | TABLE XIII     |
| Estimated Wearable Component Costs     | TABLE XIV      |

Chapter XIV contains no tables. If Chapter XV retains its hardware-cost summary table, that becomes TABLE XV. The LoRaWAN energy table should be removed from Chapter XV because it is now included in Chapter XII.

Next available identifiers after Chapter XV: TABLE XVI and Fig. 15.

This completes the missing analytical stationary-node power-budget section. The professor's requirement is now addressed at the design-calculation level, while experimental verification remains outstanding.
