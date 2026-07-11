# Design Notes

## DN-006 — Implementation Card

> *Translate design into code.*

---

# Tool

- [x] ggplot2
- [ ] Plotly
- [ ] Power BI
- [ ] Tableau
- [ ] Python
- [ ] Other

---

# Why this tool?

* `ggplot2` (within the R ecosystem) is built strictly on the **"Grammar of Graphics"**. It allows for a layered, declarative approach to building charts, which perfectly mirrors our Design Mapping Card (DN-004). 
* It provides absolute control over non-data ink via customizable `theme()` functions, enabling the extreme decluttering required for our projector presentation.
* It natively supports complex transformations like `facet_grid()` (for Small Multiples) and `coord_polar()` (for radial Wind Roses) without breaking the underlying data structure.
* Working in R Markdown ensures **100% reproducibility**. The final charts will be programmatically knitted into the report without error-prone, manual "copy-pasting" of screenshots.

---

# Implementation plan

Step 1: Data Preparation & Engineering

* Import the raw CSV data using `readr`. Convert time strings into proper `POSIXct` objects. Decode the `coco` numerical column into descriptive categorical factors ("Clear", "Rain") to prevent the artificial ordering trap. Mathematically bin the continuous wind direction (`wdir`) into 8 categorical compass factors (N, NE, E...).

Step 2: Layering the Geometries (Base Canvas)

* **Chart 1 (Chronology):** Create a long-format dataframe, map time to the X-axis, and use `geom_line()` layered with `facet_grid()` to cleanly stack Atmospheric Pressure and Air Temperature.
* **Chart 2 (Wind Rose):** Summarize the data by wind compass direction. Map frequency to Y, average temperature to `fill`, use `geom_col()`, and apply the magic layer: `coord_polar()`.

Step 3: Aesthetic Refinement & Decluttering (Tufte's Rules)

* Maximize the Data-Ink Ratio by applying `theme_minimal()`, removing heavy background grids and redundant legends.
* Apply colorblind-safe, perceptually uniform palettes (e.g., Viridis "Magma" for heat).
* Add direct text annotations (`geom_text` with `parse = TRUE`) on the Wind Rose petals to explicitly show precise temperature values, completely bypassing the cognitive difficulty of estimating values on a radial axis.

---

# Notes

* To ensure maximum readability for the final pitch in the Katowice conference room, we will set global R Markdown chunk options (e.g., `dpi = 300`, `fig.width = 10`) to render high-resolution, crisp graphics perfectly scaled for a large projector screen.
