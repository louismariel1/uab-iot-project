mermaid
```

flowchart TB
    CLOUD["☁️ CLOUD TIER<br/>Historical Analytics • Cloud AI • Storage • Alert Services<br/>Spatial Heatmaps • Multi-device Correlation • APIs"]

    EDGE["⚙️ EDGE TIER<br/>Event Fusion • Edge AI • Geofence Evaluation • Buffering<br/>Offline Operation • Risk Scoring • Data Filtering"]

    DEVICE["📡 DEVICE TIER<br/>Motion/Position Sensors • ULP MCU • Local Processing<br/>Local AI • Event Detection • Temporary Storage<br/>Adaptive Sensing • Device-State Monitoring"]

    PERSON(["🛡️ Protected Person / Environment"])

    CLOUD <-->|"🔒 Secure wide-area connection"| EDGE
    EDGE <-->|"📶 Low-power local connection"| DEVICE
    DEVICE --> PERSON

    classDef cloud fill:#D6EAF8,stroke:#2471A3,stroke-width:2px,color:#154360
    classDef edge fill:#D5F5E3,stroke:#239B56,stroke-width:2px,color:#145A32
    classDef device fill:#FCF3CF,stroke:#D4AC0D,stroke-width:2px,color:#7D6608
    classDef person fill:#F5B7B1,stroke:#C0392B,stroke-width:2px,color:#78281F

    class CLOUD cloud
    class EDGE edge
    class DEVICE device
    class PERSON person

    linkStyle 0 stroke:#2471A3,stroke-width:2px
    linkStyle 1 stroke:#239B56,stroke-width:2px
    linkStyle 2 stroke:#C0392B,stroke-width:2px
```

### Color scheme

- Blue — Cloud tier: Analytics, AI, storage, alerts, and APIs.
- Green — Edge tier: Real-time fusion, local AI, risk scoring, and offline operation.
- Yellow — Device tier: Sensors, microcontroller, local processing, and event detection.
- Red — Protected person/environment: The monitored endpoint.

### How to use it on GitHub

1. Open your `README.md` or another Markdown file.
2. Paste the Mermaid code inside a fenced code block beginning with ```` ```mermaid ```` and ending with ```` ``` ````.
3. Commit or preview the file. GitHub will render the diagram with colors and arrows.

Note: The arrows between the cloud, edge, and device tiers are bidirectional, reflecting the two-way connections in your architecture. The device-to-person connection is directional. If you need strictly one-way data flow between tiers, replace `<-->` with `-->`.
