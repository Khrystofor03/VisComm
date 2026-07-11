# Design Notes

## DN-001 — Dataset Card

> *Understand your data before designing a visualization.*

---

# Dataset

**Title**

Katowice Hourly Weather Data (June 2026)

**Source**

Meteostat (Weather Station: Katowice / Muchowiec, ID: 12560)

**Author / Organization**

Meteostat (aggregating open data from national weather services like NOAA and DWD).

**URL**

https://meteostat.net/en/station/12560?t=2026-06-01/2026-06-30

---

# Description

This dataset contains hourly meteorological observations for Katowice, Poland, covering the entire month of June 2026 (720 records in total). It captures complex environmental variables including air temperature, relative humidity, atmospheric pressure, wind dynamics, and specific weather condition codes, providing a comprehensive picture of summer climate anomalies.

---

# Observations

One row represents the exact meteorological conditions recorded during one specific hour (e.g., 2026-06-01 14:00:00) at the Katowice weather station.

---

# Variables

| Variable | Type       | Description |
|----------|------------|-------------|
| `time`   | Temporal   | Date and hour of the observation (YYYY-MM-DD HH:MM:SS) |
| `temp`   | Continuous | Air temperature in °C |
| `dwpt`   | Continuous | Dew point in °C |
| `rhum`   | Continuous | Relative humidity in % |
| `prcp`   | Continuous | Precipitation amount in millimeters |
| `snow`   | Continuous | Snow depth in millimeters |
| `wdir`   | Continuous | Wind direction in degrees (0-360) |
| `wspd`   | Continuous | Average wind speed in km/h |
| `wpgt`   | Continuous | Wind peak gust in km/h |
| `pres`   | Continuous | Atmospheric sea-level pressure in hPa |
| `tsun`   | Continuous | Total sunshine duration in minutes |
| `coco`   | Categorical| Weather condition code (originally encoded as integers 1-27) |

---

# Data quality

## Missing values

* The dataset contains a significant amount of missing values (NA / empty fields) in specific columns, particularly `snow` and `tsun` (sunshine duration), which are mostly unrecorded or irrelevant for June. These columns will be excluded from the analysis.

## Outliers

* Air temperature (`temp`) shows extreme, highly asymmetric positive outliers, reaching peaks up to 36°C in the last week of the month. 

## Potential bias

* The data relies on a single specific station (Katowice / Muchowiec, usually located near the airport/urban border). This may introduce an "urban heat island" bias, meaning recorded temperatures might be slightly higher and less volatile than in the surrounding rural Silesian areas.

## Other issues & Engineering Needs

* **Artificial Ordering Trap:** The `coco` (weather condition) variable is originally stored as numerical data (1 to 27). It must be explicitly converted to categorical factors ("Clear", "Rain", etc.) to prevent algorithms from calculating meaningless statistics.
* **Continuous to Categorical Transformation:** The wind direction (`wdir`) is provided in continuous degrees (0-360). For meaningful radial visualization (Wind Rose), it must be engineered into categorical compass directions (N, NE, E, SE, S, SW, W, NW).

---

# Initial observations

Following an extensive Exploratory Data Analysis (EDA), our initial assumptions have evolved into a much deeper meteorological narrative:

* **The Heatwave Anomaly:** Katowice experienced a severe heatwave in the final week of June 2026. While the median temperature was a comfortable 18°C, the late-month peaks shattered the 35°C mark.
* **Correlations:** There is a massive negative correlation (-0.83) between Temperature and Relative Humidity (`rhum`), meaning the extreme heat was dry, not tropical.
* **Pressure as a Leading Indicator:** Time-series analysis reveals that the heatwave was directly preceded by a massive build-up of atmospheric pressure (`pres`), stabilizing over 1020 hPa (a blocking anticyclone) which cleared the skies.
* **The Origin of Heat:** The Wind Rose radial analysis uncovered a critical insight. While Katowice is predominantly cooled by Westerly (W) and South-Westerly (SW) winds (averaging ~16°C), the extreme heat was "imported." Rare, but intense Southerly (S) and South-Easterly (SE) winds brought blistering thermal masses averaging 20-22°C even during non-peak hours.
* **Cloud Cover Effect:** Ridgeline distributions prove that extreme temperature spikes (>30°C) occurred *exclusively* under "Clear" and "Fair" sky conditions (`coco`).

---

# Notes

* **Design Strategy Shift:** Initially, the plan was to declutter the dataset by dropping `wdir` and `pres`. However, EDA proved these variables are the fundamental physical drivers of the temperature spikes. They have been upgraded to **High Importance**. 
* The final presentation will focus on **"The Anatomy of a Heatwave"**, utilizing a dual-chart storytelling approach:
  1. A chronological timeline linking the pressure build-up and clear skies to the severe temperature spikes.
  2. A radial "Wind & Heat Rose" to visually explain the geographical origin of the extreme heat to the audience.
