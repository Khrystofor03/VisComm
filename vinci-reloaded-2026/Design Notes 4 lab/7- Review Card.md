# Design Notes

## DN-007 — Review Card

> *Every visualization deserves a review.*

---

# Checklist

## Message

- [x] Clear *(The narrative of the pressure dome and Southern wind acting as a thermal pump is straightforward and strongly supported).*
- [x] Focused *(Eliminated irrelevant variables like snow, dew point, and sunshine duration to maintain high Data-Ink ratio).*
- [x] Honest *(Used continuous, unmanipulated axes for time and temperature. Resisted the unethical dual Y-axis trap by using `patchwork`).*

---

## Audience

- [x] Appropriate *(Academic and professional enough for the jury, yet visually engaging due to animations and drill-downs).*
- [x] Easy to understand *(Pre-attentive color highlighting instantly guides the eye to the heatwave zone).*

---

## Design

- [x] Good hierarchy *(1. Extreme heat [Color], 2. Macro-trend [LOESS smooth lines], 3. Exact values [Text labels & Tooltips]).*
- [x] Good labels *(Direct labeling with dynamic offsets on the Wind Rose eliminates the need to constantly check legends).*
- [x] Good colors *(Viridis 'Magma' palette is colorblind-safe and semantically matches the concept of heat).*
- [x] No unnecessary elements *(Tufte's Data-Ink ratio maximized: background grids minimized, redundant UI elements stripped).*

---

## Technical

- [x] Correct scales *(Time on continuous X-axis; Wind mapped correctly to a 360-degree polar coordinate system).*
- [x] Correct legends *(Legends removed in favor of direct text annotations and hover tooltips).*
- [x] Good aspect ratio *(Wide formats selected for the projector screen in the Katowice conference room).*
- [x] High quality export *(Fully responsive HTML standalone file with embedded JavaScript via `plotly`, no external server needed).*

---

# Reflection

What worked?

* **The "Shneiderman Suite" Implementation:** Combining static `patchwork` plots for the macro-overview with `plotly` dropdowns for micro drill-downs worked flawlessly. It allowed us to pack 720 hours of data into a clean interface without the "Cluttered Chart Trap."
* **Signal vs. Noise (LOESS):** Applying LOESS smoothing curves directly over the raw time-series data perfectly resolved the issue of "jagged" visual noise, exposing the underlying physical macro-trend (the pressure dome building up) without hiding the absolute 36°C peaks.
* **Serverless Interactivity:** Using `plotly`'s `updatemenus` and `frame` animations allowed us to build a rich, interactive dashboard directly into a standalone HTML file, bypassing the need for a complex Shiny backend.
* **Overcoming Polar Coordinate Flaws:** Radial charts are typically criticized because human brains struggle to estimate curved lengths. By injecting exact, mathematically parsed labels (`parse = TRUE`) with a dynamic offset (`max * 0.08`), we completely bypassed this cognitive limitation.

---

What should be improved?

* **Contextual Baseline:** The charts definitively prove that 36°C is extremely hot, but they lack a *historical average* baseline for June in Katowice (e.g., the 10-year mean). Without this historical context, the audience cannot visually quantify the exact statistical magnitude of the anomaly.
* **Cognitive Load of Animation:** While the animated "Temperature Clock" is visually striking and engages the audience, tracking changing values on a circular axis dynamically can be cognitively demanding. Adding more user controls (like dynamically slowing down the frame rate) could improve analytical precision during the pitch.

---

Next version

* **Socio-Environmental Integration:** I would integrate Air Quality Index (AQI / PM2.5) data. Heatwaves and high-pressure blocking domes in Silesia are often accompanied by severe air stagnation and smog. Overlaying AQI data onto the Wind Rose would elevate this from a meteorological report to a powerful socio-environmental analysis.
* **Live API Pipeline:** Instead of reading a static `katowice_weather.csv`, the next version of this R Markdown document would feature a data-ingestion script connecting directly to the Meteostat JSON API, transforming this project into a live, self-updating Katowice Summer Dashboard.
