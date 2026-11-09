# Teleoperation latency calculator

**Live:** https://robopilots-ai.github.io/teleop-latency-calculator/ · also on [Hugging Face](https://huggingface.co/spaces/robopilots-ai/teleop-latency-calculator) and [robopilots.ai](https://www.robopilots.ai/tools/teleop-latency-calculator?utm_source=github&utm_medium=referral&utm_campaign=latency-calculator)

The same calculator as [robopilots.ai/tools/teleop-latency-calculator](https://www.robopilots.ai/tools/teleop-latency-calculator?utm_source=github&utm_medium=referral&utm_campaign=latency-calculator), built from the RoboPilots site's own code into a static page (`index.html`, `app.js`, `app.css`). It estimates the round-trip delay a remote robot operator will feel and shows which control mode each robot type supports at that delay.

**Inputs**

- Operator and robot locations (45 cities across North America, Europe, Latin America, Asia, Africa and Oceania), a manual one-way distance, or a measured ping between the two sites.
- Network at the robot and at the operator: fiber/cable, 5G, 4G LTE, Starlink, GEO satellite or LAN, each with a sourced typical overhead you can edit.
- Video and control pipeline (capture, encode, decode, display, controller). The 60 ms default is editable.
- Route inefficiency factor (default 1.5).

**Output**

- Estimated round trip with a breakdown.
- One of six bands (< 50, 50–150, 150–300, 300–700, 700–1000, > 1000 ms).
- The control mode the published evidence supports at that band for robot arms, humanoids, quadrupeds, wheeled robots and vehicles, drones and other robots: direct control, assisted control, move and wait, or supervision. Each comes with numbered sources.

## Method

Round trip = propagation + robot-side network + operator-side network + pipeline.

Propagation uses the great-circle (haversine) distance and light in fiber at about 2/3 c (≈ 199.9 km/ms, or 5 µs/km as in ITU-T G.114). That figure is doubled for the round trip and multiplied by the route factor. New York to London (≈ 5,570 km) gives ≈ 56 ms of pure round-trip propagation, or ≈ 84 ms at 1.5×.

Network defaults come from Ookla (5G 2026 benchmark; Starlink, Hughesnet and Viasat Q1 2026), a 2024 review of teleoperation over LTE (Kamtam et al., Sensors), FCC Measuring Broadband America and ITU-T G.114. The band-to-mode table follows the [RoboPilots teleoperation latency guide](https://www.robopilots.ai/guides/teleoperation-latency) and the studies it cites. The full list of sources is on the page.

These are estimates and rules of thumb. Measure glass-to-glass on your real link: point the robot camera at a millisecond clock on the operator's screen and photograph both.

## Run locally

Serve the folder (for example `python3 -m http.server`) and open `index.html`. Your inputs never leave the browser; only the robot images load from robopilots.ai.

## GitHub Pages copy

The same files are published on GitHub Pages. On a `*.github.io` host, every RoboPilots link switches to `utm_source=github` automatically, for example:

```
https://www.robopilots.ai/?utm_source=github&utm_medium=referral&utm_campaign=latency-calculator
```

On any other host the links are tagged `utm_source=huggingface`.

---

Built by [RoboPilots](https://www.robopilots.ai/?utm_source=github&utm_medium=referral&utm_campaign=latency-calculator): managed remote operators trained on your robot; one-week trial with a clean-episodes-per-operator-hour baseline.

License: MIT.
