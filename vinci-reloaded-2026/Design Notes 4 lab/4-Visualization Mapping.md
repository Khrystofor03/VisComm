# Design Notes

## DN-004 — Visualization Mapping Card

> *Translate data into visual language.*

---

# Data → Visual mapping

| Data | Visual encoding | Why? |
|------|-----------------|------|
| `datetime` & `wind_compass` | Position (X-axis & Angular) | **Time (`datetime`)** is naturally mapped left-to-right on the X-axis for chronological reading. **Compass direction** is mapped to angular position (Polar coordinates) to match real-world spatial mental models. |
| `temp` & Wind Frequency | Length / Position (Y-axis) | Position on a linear Y-axis is the most accurate visual attribute for decoding quantitative data like **temperature**. In the radial chart, the length of the petals perfectly encodes the **frequency (hours)** of wind. |
| *N/A* | Area | Avoided. Human brains struggle to accurately compare 2D areas (as learned from the Pie/Bubble chart critique). |
| Heatwave Anomaly (`temp`) | Color (Hue & Intensity) | We use a **Diverging/Sequential palette** (e.g., Magma or Red vs. Gray). Extreme heat (>30°C) is mapped to intense red/orange to pre-attentively *drive attention*, while normal temperatures remain neutral gray. |
| *N/A* | Shape | Avoided to minimize chartjunk. We rely on lines and bars rather than individual point markers (to prevent overplotting). |
| Non-heatwave data | Opacity (Alpha) | Lower opacity (transparency) will be used for the atmospheric pressure curve and non-heatwave days to push them to the visual background, enhancing hierarchy. |
| `temp` & `pres` | Facets (Small Multiples) | Stacked vertically. This allows the audience to compare pressure drops/spikes with temperature changes on the same timeline without the confusion of a dual Y-axis. |
| *N/A* | Animation | Static presentation. Due to the projector medium, static, high-contrast charts are safer and allow the speaker to control the narrative pacing. |

---

# Visual hierarchy

First

* **The Extreme Heat Anomaly:** The viewer's eyes will instantly snap to the bright red/orange peaks on the timeline (late June) and the intensely colored Southern petals on the Wind Rose, guided by color contrast (Pre-attentive processing).

Second

* **The Shape and Direction (The Context):** The overall wave-like trend of the temperature line and the massive length of the Westerly wind petals, setting the baseline normal conditions.

Third

* **The Underlying Physics (Details-on-Demand):** The atmospheric pressure line (muted in the background) and the specific axis labels/text annotations explaining the exact degrees and dates.

---

# Accessibility

- [x] Colorblind-friendly *(Using verified Viridis/ColorBrewer palettes like Magma, avoiding Red-Green conflicts)*
- [x] Good contrast *(Dark, bold colors for the main data-ink against a pure white background)*
- [x] Readable labels *(Large, Sans-Serif fonts, e.g., 16pt+ Arial or Montserrat, avoiding vertical/rotated text)*
- [x] Appropriate font size *(Optimized specifically for a projector screen in a large conference room)*

---

# Notes

* **Dual-Chart Strategy (Shneiderman's Mantra):** 
  1. **Overview First:** A faceted timeline (Chronology) showing the macro-trend of pressure building up and triggering the heatwave.
  2. **Zoom / Filter:** A Radial Wind Rose focusing specifically on the mechanics of the heat (proving the heat was imported by Southern winds).
* **Data-Ink Maximization (Tufte):** All redundant grid lines, panel borders, and unnecessary legends will be stripped via `theme_minimal()` and `theme_void()`. Exact temperature values will be directly labeled on the Wind Rose to eliminate the need for cognitive context-switching between the chart and a legend.
