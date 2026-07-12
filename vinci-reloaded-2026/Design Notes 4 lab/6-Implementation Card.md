# Design Notes

## DN-006 — Implementation Card

> *Translate design into code.*

---

# Tool

- [x] ggplot2
- [x] Plotly
- [ ] Power BI
- [ ] Tableau
- [ ] Python
- [x] Other (patchwork, R Markdown)

---

# Why this tool?

* `ggplot2` provides absolute programmatic control over non-data ink via customizable `theme()` functions, and its declarative "Grammar of Graphics" approach makes it perfect for our static, highly customized charts (like the radial Wind Rose).
* `Plotly` seamlessly upgrades static R charts into interactive web components without requiring a dedicated Shiny backend server. It allows us to build complex Dropdown Menus for data drill-downs and implement frame-based animations directly within a standalone HTML file.
* `patchwork` is the ultimate ethical solution to the "Dual Y-Axis" problem, allowing us to flawlessly align and stack the timeline of Atmospheric Pressure and Temperature on a shared X-axis.
* Working in R Markdown ensures **100% reproducibility**. The raw data flows directly into the final HTML presentation, eliminating error-prone, manual "copy-pasting" of screenshots.

---

# Implementation plan

Step 1: Data Preparation & Engineering

* Import the raw CSV data using `readr`. Convert time strings into `POSIXct` objects. 
* Decode the `coco` numerical column into descriptive categorical factors to prevent the artificial ordering trap. 
* Mathematically bin the continuous wind direction (`wdir`) into 8 categorical compass factors.
* **Feature Engineering for Interactivity:** Create formatted `hour_label` (e.g., "14:00") and `date_label` columns. Pre-calculate daily aggregated summaries (max temp, avg pressure) to serve as the baseline traces for our Plotly drill-downs.

Step 2: Layering the Geometries & Interactivity

* **The Overview (ggplot2 + patchwork):** Construct two separate line charts for Pressure and Temperature. Add `geom_smooth(method = "loess")` to extract the macro-trend from the micro-noise. Use conditional coloring and `annotate("rect")` to highlight the heatwave, then stack them using `patchwork`.
* **The Drill-Downs (Plotly):** Initialize an empty `plot_ly()` object. Add the daily overview as the base trace, then use a `for` loop to inject 30 hidden hourly traces. Construct an `updatemenus` dropdown to toggle trace visibility, allowing the user to zoom from the daily macro view into specific hourly micro views.
* **The Spatial Origin (ggplot2):** Group data by wind direction, map average temperature to `fill`, and apply `coord_polar()`. Calculate a dynamic offset (`max * 0.08`) to ensure direct text labels never overlap with the geometries.
* **The Diurnal Clock (Plotly):** Use `plot_ly(type = 'scatterpolar')`, mapping hours around the clock face (`theta`) and temperature to the radius (`r`). Inject the `frame` argument to automatically generate a Play button and animate the daily rhythm.

Step 3: Aesthetic Refinement & Decluttering (Tufte's Rules)

* Maximize the Data-Ink Ratio by applying `theme_minimal()`, removing heavy background grids and redundant legends.
* Apply colorblind-safe, perceptually uniform palettes (Viridis "Magma" for heat profiling).
* **Encoding Safety:** Use HTML entities (`&#176;`) in Plotly and mathematical parsing (`parse = TRUE`) in ggplot2 to securely render degree symbols across all operating systems and browsers without encoding crashes.

---

# Notes

* To accommodate the Plotly JavaScript dependencies and the interactive UI elements (Dropdowns, Sliders, Hover-tooltips), the R Markdown output must be set strictly to `html_document`. 
* Global chunk options (`dpi = 300`, `fig.width = 10`) will guarantee that the static ggplot elements render crisp and perfectly scaled for the large projector screen in the Katowice conference room.
