# Design Notes

## DN-004 — Visualization Mapping Card

> *Translate data into visual language.*

---

# Data → Visual mapping

| Data | Visual encoding | Why? |
|------|-----------------|------|
| `datetime` & `wind_compass` & `hour` | Position (X-axis & Angular) | **Time (`datetime`)** is naturally mapped left-to-right on the Cartesian X-axis for chronological reading. **Compass direction** and **24-Hour cycles** are mapped to angular positions (Polar coordinates) to perfectly match real-world spatial and cyclical mental models. |
| `temp` & `pres` & Wind Frequency | Length / Position (Y-axis / Radius) | Position on a linear Y-axis is the most accurate visual attribute for decoding quantitative data. In our radial charts (Wind Rose & Temp Clock), the length of the petals/radius encodes frequency and magnitude seamlessly. |
| *N/A* | Area | Avoided. Human brains struggle to accurately compare 2D areas (as learned from the Pie/Bubble chart critique). |
| Heatwave Anomaly & Macro-Trends | Color (Hue & Intensity) | We use conditional coloring (`temp >= 28` is Red) and background enclosure (Red rectangle) to pre-attentively *drive attention* to the heatwave. A continuous 'Magma' palette highlights the hot Southern winds. Bright Cyan and Orange highlight the LOESS trendlines. |
| Macro-Trend extraction | Smoothing (LOESS Curve) | Applying Gestalt's Law of *Prägnanz* (Simplicity). We map the underlying macro-trend of pressure and temperature to a smoothed LOESS curve, filtering out hourly micro-noise. |
| Hourly Details | Interactivity (Hover Tooltips & Dropdowns) | Applying Shneiderman's Mantra. By using Plotly dropdowns, we map chronological aggregation (Daily Max/Avg vs. Hourly) to user interaction, preventing chart clutter. |
| The Diurnal Cycle (`date_label`) | Animation (Frames) | Mapped to Plotly animation frames. Instead of drawing 30 overlapping circles for 30 days, animation uses the natural flow of time to show the daily breathing rhythm of the city's temperature. |

---

# Visual hierarchy

First

* **The Extreme Heat Anomaly:** The viewer's eyes will instantly snap to the bright red peaks, the semi-transparent red background enclosure spanning late June, and the brilliantly colored hot Southern petals on the Wind Rose, guided by stark color contrast (Pre-attentive processing).

Second

* **The Macro-Trends (The Context):** The smooth Cyan (Pressure) and Orange (Temperature) LOESS trendlines that cut through the visual noise, establishing the underlying physical relationship between the two variables.

Third

* **The Exact Physics (Details-on-Demand):** The exact temperature labels strategically placed above the Wind Rose petals (using dynamic offsets) and the hover-tooltips in the Plotly charts, providing precise numerical context without cluttering the main view.

---

# Accessibility

- [x] Colorblind-friendly *(Using verified Viridis 'Magma' palette, avoiding standard Red-Green conflicts).*
- [x] Good contrast *(Bright Cyan and Orange trendlines stand out sharply against the neutral gray hourly data lines).*
- [x] Readable labels *(Dynamic calculating of label offsets `max * 0.08` ensures text never overlaps with geometries. Mathematical parsing `parse = TRUE` ensures cross-platform rendering of degree symbols without encoding errors).*
- [x] Appropriate font size *(Optimized specifically for a projector screen using bold fonts and clean `theme_minimal()` setups).*

---

# Notes

* **Shneiderman's Mantra Mastered:** The presentation is strictly structured around:
  1. **Overview First:** The `patchwork` timeline showing the macro-trend (LOESS) of the Pressure Dome triggering the heatwave.
  2. **Zoom / Filter:** The interactive Plotly dropdowns allowing the jury to drill down into specific days from a daily overview.
  3. **Details-on-Demand:** Tooltips via hover and direct numerical labeling on the Wind Rose.
* **Data-Ink Maximization (Tufte):** Legends were deliberately removed (`legend.position = "none"`) from the Wind Rose and Timeline. Color serves as a direct indicator, and exact values are placed directly on the data points, eliminating the cognitive friction of glancing back and forth between a legend and the chart.
