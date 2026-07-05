# Design Notes

## DN-003 — Data Understanding Card

> *Understand relationships before choosing a chart.*

---

# Variables

List the variables you plan to use.

| Variable | Type | Importance |
|----------|------|------------|
| `time` (Date & Hour) | Temporal | High |
| `temp` (Temperature) | Continuous | High |
| `coco_label` (Weather condition) | Categorical | High |

---

# Relationships

What relationships are interesting?

* The temporal progression of temperature throughout the day and night (the diurnal cycle).
* The connection between specific weather conditions (e.g., Clear vs. Cloudy) and the intensity of temperature spikes.

---

# Possible comparisons

* Comparing peak daily temperatures across different days of the month.
* Comparing the shape of the temperature curve on a "Clear" day versus a "Rain" or "Overcast" day.
* Comparing daytime maximums with nighttime minimums (temperature amplitude).

---

# Possible trends

* The daily wave-like (sinusoidal) trend of temperatures rising in the afternoon and dropping at night.
* A potential overarching heatwave trend (a build-up of heat over several consecutive days in June).

---

# Possible distributions

* The frequency of extreme heat hours (>25°C or >30°C) versus comfortable hours.
* The proportion of sunny/clear hours versus cloudy or rainy hours during the month.

---

# Possible correlations

* Lack of cloud cover (Clear/Fair conditions) is likely strongly correlated with higher daily maximum temperatures.
* Overcast or rainy conditions might correlate with a "flatter" temperature curve (lower maximums, but potentially higher minimums at night due to the greenhouse effect of clouds).

---

# Hypotheses

What do you expect to discover?

* I expect to discover that the absolute highest temperature peaks (the most severe heatwaves) occur strictly during "Clear" or "Fair" sky conditions in the mid-to-late afternoon. 
* I also hypothesize that rainy or heavily clouded days will show a significantly lower temperature amplitude (less difference between day and night).
