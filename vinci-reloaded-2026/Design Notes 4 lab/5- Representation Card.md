# Design Notes

## DN-005 — Representation Card

> *Explore different ways of communicating the same information.*

---

# Candidate representations

- [x] Option A: Dual Y-Axis Line Chart (Pressure & Temp superimposed)
- [x] Option B: Grouped Boxplots (Temp distribution by Wind Direction)
- [x] Option C: Dual-Chart Approach (Faceted Time-Series + Radial Wind Rose)

---

# Sketch A

*Draw (Mental Sketch).* 
A single line chart with Time on the X-axis. Temperature (red line) uses the left Y-axis, and Atmospheric Pressure (blue line) uses the right Y-axis.

Why?

* **Pros:** Combines the two most important chronological variables into one space, showing how pressure drops/spikes align with temperature.
* **Cons (Fatal Flaw):** Dual Y-axes are notoriously misleading and violate core data visualization ethics. By artificially manipulating the scales of the left and right axes, the creator can force lines to cross anywhere, creating false visual correlations. This creates severe cognitive overload and is highly discouraged in modern visual analytics.

---

# Sketch B

*Draw (Mental Sketch).* 
A traditional Cartesian (X-Y) grid. The X-axis has 8 categorical compass directions (N, NE, E...). The Y-axis shows Temperature. The data is represented as Boxplots or Violin plots for each wind direction.

Why?

* **Pros:** Excellent for showing statistical distributions, outliers, and medians of temperature for each wind direction.
* **Cons:** It completely destroys the natural *spatial mental model* of the audience. Humans intuitively think of wind directions as a circle (a compass). Mapping a circle onto a flat, linear X-axis creates friction. Furthermore, it completely loses the chronological story (the build-up of the heatwave over time).

---

# Sketch C

*Draw (Mental Sketch).* 
A two-part visual story. 
Part 1: A faceted line chart (Small Multiples). Top panel shows Pressure, bottom panel shows Temperature (with extreme peaks highlighted in red). 
Part 2: A Radial Column Chart (Wind Rose) using `coord_polar`. Length encodes wind frequency, color intensity encodes average temperature, and exact values are directly labeled on the petals.

Why?

* **Pros:** Faceting perfectly solves the "Dual Y-Axis" trap—allowing safe, synchronized comparison over time. The Radial Wind Rose aligns perfectly with human geographical intuition. Direct text labeling on the petals eliminates the cognitive flaw of polar coordinates (humans being bad at estimating curved areas/lengths).
* **Cons:** Takes up more screen real estate, requiring careful layout design for the presentation slides.

---

# Decision

Chosen representation:

* **Option C:** The Dual-Chart Narrative (Faceted Time-Series & Radial Wind Rose).

Why?

* It perfectly balances the two questions of our narrative: *"When/How did the heatwave happen?"* (answered by Gestalt continuity of the faceted lines) and *"Where did the heat come from?"* (answered by the spatial mapping of the Wind Rose). 
* By separating the chronological story from the geographical/wind story, we avoid the "Cluttered Chart Trap." Every visual attribute strictly supports the communication goal while maintaining a maximized Data-Ink Ratio.
