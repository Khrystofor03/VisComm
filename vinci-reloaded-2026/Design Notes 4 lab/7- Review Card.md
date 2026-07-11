# Design Notes

## DN-007 — Review Card

> *Every visualization deserves a review.*

---

# Checklist

## Message

- [x] Clear *(The narrative of the pressure dome and Southern wind acting as a thermal pump is straightforward).*
- [x] Focused *(Eliminated irrelevant variables like snow, dew point, and sunshine duration).*
- [x] Honest *(Used continuous, unmanipulated axes for time and temperature. Did not use misleading dual Y-axes).*

---

## Audience

- [x] Appropriate *(Academic and professional enough for the jury, yet visually intuitive).*
- [x] Easy to understand *(Pre-attentive color highlighting instantly guides the eye to the heatwave).*

---

## Design

- [x] Good hierarchy *(1. Extreme heat [Color], 2. Wind direction [Spatial/Polar], 3. Exact values [Text labels]).*
- [x] Good labels *(Direct labeling on the Wind Rose eliminates the need to constantly check legends).*
- [x] Good colors *(Viridis 'Magma' palette is colorblind-safe and semantically matches the concept of heat).*
- [x] No unnecessary elements *(Tufte's Data-Ink ratio maximized: grids minimized, legends removed where redundant).*

---

## Technical

- [x] Correct scales *(Time on continuous X-axis; Wind mapped correctly to a 360-degree polar coordinate system).*
- [x] Correct legends *(Legends removed in favor of direct text annotations).*
- [x] Good aspect ratio *(Wide formats selected for the projector screen in the Katowice conference room).*
- [x] High quality export *(Vector-based generation via `knitr` with `dpi = 300`).*

---

# Reflection

What worked?

* **The Dual-Chart Narrative:** Splitting the story into two charts (Chronological Timeline + Spatial Wind Rose) prevented the "Cluttered Chart Trap". 
* **Overcoming Polar Coordinate Flaws:** Radial charts (like the Wind Rose) are typically criticized because human brains struggle to estimate curved lengths. By injecting exact R-parsed mathematical labels directly onto the petals (`parse = TRUE`), we completely bypassed this cognitive limitation. 
* **Pre-attentive Encoding:** Using the 'Magma' palette specifically for Southern winds immediately triggered the visual association with heat, proving the hypothesis with almost zero cognitive effort from the viewer.

---

What should be improved?

* **Data Density on the Timeline:** The faceted time-series chart plots 720 individual hourly points. While this shows the exact diurnal (day/night) cycles, the lines are quite jagged and dense. Applying a smoothing technique (like a 24-hour rolling average) could reduce visual noise, though we consciously chose not to do this to preserve the visibility of the absolute extreme 36°C peaks.
* **Contextual Baseline:** The charts show that 36°C is hot, but they don't show the *historical average* for June in Katowice. Without a historical baseline, the audience doesn't visually know *how much* of an anomaly this heatwave truly was.

---

Next version

* **Interactive Dashboard:** If this were not constrained to a static projector presentation, the next version would transform these static `ggplot2` charts into an interactive `Shiny` application or `plotly` dashboard, allowing users to hover over exact hours to see tooltip data (Details-on-Demand).
* **Adding External Datasets:** I would integrate Air Quality Index (AQI / PM2.5) data. Heatwaves in Silesia are often accompanied by specific air quality changes, and overlaying smog data onto the Wind Rose would create a powerful socio-environmental analysis.
