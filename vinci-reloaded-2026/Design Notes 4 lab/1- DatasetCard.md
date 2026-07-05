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

This dataset contains hourly meteorological observations for Katowice, Poland, covering the entire month of June 2026 (720 records in total). It includes multiple environmental variables such as air temperature, relative humidity, precipitation, wind speed, and specific weather condition codes.

---

# Observations

One row represents the exact weather conditions recorded during one specific hour (e.g., 2026-06-01 14:00:00) at the Katowice weather station.

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

* The dataset contains a significant amount of missing values (NA / empty fields) in specific columns, particularly `snow` and `tsun` (sunshine duration), which seem to be unrecorded for most hours in June.

## Outliers

* Temperature (`temp`) reaches extreme peaks (up to 36°C), which is unusually hot but realistic for summer heatwaves in Central Europe.

## Potential bias

* The data relies on a single specific station (Katowice / Muchowiec, usually located near the airport or urban border). This might include an "urban heat island" effect, meaning the temperatures might be slightly higher than in the surrounding rural areas.

## Other issues

* **Artificial Ordering Trap:** The `coco` (weather condition) variable is originally stored as numerical data (1 to 27). It must be explicitly converted to categorical factors during data preparation to prevent algorithms from calculating meaningless statistics (like "average weather condition = 3.5").

---

# Initial observations

* Based on the initial exploratory data analysis (EDA), Katowice experienced highly variable temperatures in June 2026, ranging from a chilly 6°C to a scorching 36°C.
* The most frequent temperatures recorded were surprisingly mild (13°C - 15°C).
* According to the weather condition codes (`coco`), the dominant state of the sky was "Fair" (288 hours) and "Cloudy" (158 hours), meaning clear skies or light clouds dominated the month, though there were also 50 hours of light rain.

---

# Notes

* Before creating the final visualization, the dataset should be simplified (decluttered) by dropping unused columns like `wdir`, `pres`, and `dwpt` to maximize the data-ink ratio and focus purely on the relationship between time, temperature, and cloud cover.
