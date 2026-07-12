# Design Notes

## DN-005 — Representation Card

> *Explore different ways of communicating the same information.*

---

# Candidate representations

- [x] Option A: Dual Y-Axis Line Chart & Linear Heatmap (The Standard Approach)
- [x] Option B: Cartesian Boxplots & 30-Panel Facet Grid (The Statistical Approach)
- [x] Option C: The "Shneiderman Suite" (Patchwork Overview + Plotly Drill-downs + Radial Animations)

---

# Sketch A

*Draw (Mental Sketch).* 
1. A single chronological line chart where Temperature (red) uses the left Y-axis and Pressure (blue) uses the right Y-axis. 
2. A flat 2D Heatmap where X is the day of the month, Y is the hour, and color is the temperature.

Why?

* **Pros:** Highly compact. Fits the entire month's macro and micro-trends into just two static charts.
* **Cons (Fatal Flaws):** Dual Y-axes are notoriously misleading and violate core data visualization ethics; by artificially manipulating the left/right scales, the creator can force lines to cross anywhere, creating false visual correlations. Furthermore, linear heatmaps for daily cycles make it cognitively difficult to extract precise temperature values, as the human brain struggles to decode exact quantitative numbers purely from a color gradient.

---

# Sketch B

*Draw (Mental Sketch).* 
1. A traditional Cartesian (X-Y) grid with 8 categorical compass directions (N, NE, E...) on the X-axis and Temperature on the Y-axis using Boxplots. 
2. A massive 30-panel `facet_wrap` showing a separate static line chart for each day of June.

Why?

* **Pros:** Excellent for showing exact statistical distributions, medians, and outliers without hiding any data points.
* **Cons:** It completely destroys the natural *spatial mental model* of the audience. Humans intuitively think of wind directions as a circle (a compass), not a straight line. Moreover, projecting a 30-panel facet grid on a single presentation screen will result in unreadable, microscopic charts (the "Cluttered Chart Trap"), completely failing the back-row projector test in our Katowice conference room.

---

# Sketch C

*Draw (Mental Sketch).* 
A 4-part Interactive Narrative combining static summaries with interactive deep-dives:
1. **Macro Overview:** A vertically stacked `patchwork` chart showing Pressure and Temperature over time, utilizing LOESS smoothing curves to highlight the macro-trend and a red background enclosure to highlight the heatwave.
2. **Micro Drill-down:** Bar charts using `plotly` dropdown menus to toggle between a "Daily Overview" and specific "Hourly Details".
3. **Spatial Origin:** A Radial Column Chart (Wind Rose) using `coord_polar` with dynamic, direct text labels.
4. **Diurnal Cycle:** An animated polar scatter plot (The Temperature Clock) mapping 24 hours to a circle, evolving day by day via a Play button.

Why?

* **Pros:** This approach perfectly implements Shneiderman's Mantra ("Overview first, zoom and filter, then details-on-demand"). The `patchwork` overview solves the unethical Dual Y-Axis trap. The `plotly` dropdowns solve the 30-panel clutter trap by hiding hourly details until requested. The radial charts perfectly align with human geographical (compass) and chronological (clock face) intuition.
* **Cons:** Highly demanding to code in R. It requires the output format to be an HTML document rather than a static PDF, as the JavaScript-based Plotly animations and dropdowns need a browser to function.

---

# Decision

Chosen representation:

* **Option C:** The "Shneiderman Suite" (Interactive & Radial Storytelling).

Why?

* It perfectly balances the complex questions of our narrative without overwhelming the jury. 
* *"When/How did the heatwave happen?"* is answered immediately by the Gestalt continuity of the smoothed LOESS lines on the static overview. 
* *"Where did the heat come from?"* is answered by the spatial mapping of the Wind Rose. 
* Finally, the Plotly interactivity (Dropdowns & Animations) transforms the project from a standard statistical report into an engaging, modern data product, allowing the presenter to dynamically answer detailed questions from the jury on the fly.
