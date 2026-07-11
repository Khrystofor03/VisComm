# Design Notes

## DN-003 — Data Understanding Card

> *Understand relationships before choosing a chart.*

---

# Variables

List the variables you plan to use.

| Variable | Type | Importance |
|----------|------|------------|
| `datetime` (Date & Hour) | Temporal | High |
| `temp` (Air Temperature in °C) | Continuous | High |
| `pres` (Atmospheric Pressure in hPa) | Continuous | High |
| `wind_compass` (Wind Direction) | Categorical | High |
| `coco_label` (Weather condition) | Categorical | High |
| `rhum` (Relative Humidity in %) | Continuous | Medium |

---

# Relationships

What relationships are interesting?

* **Pressure and Heat Accumulation:** How sustained high atmospheric pressure (an anticyclone) clears the skies and precedes a rapid build-up of extreme temperature.
* **Wind Direction as a Thermal Vector:** The direct relationship between specific wind origins (e.g., South vs. West) and the thermal mass they bring to Katowice.
* **Temperature and Humidity (Thermal Comfort):** The inverse relationship showing how moisture in the air drops as the heatwave peaks.

---

# Possible comparisons

* Comparing the average temperatures brought by the prevailing Westerly/South-Westerly winds against the rare, but intense Southerly winds.
* Comparing the shape and amplitude of the daily temperature curve during the stable first half of June versus the high-pressure block at the end of the month.
* Comparing peak daytime heat levels across different sky conditions ("Clear" vs. "Rain/Overcast").

---

# Possible trends

* The daily wave-like (sinusoidal) diurnal temperature cycle.
* A macro-level trend: A massive, multi-day build-up of atmospheric pressure in late June acting as a catalyst (leading indicator) for the severe heatwave that followed.

---

# Possible distributions

* **Wind Frequency vs. Temperature (The Wind Rose):** The spatial distribution showing that while Western winds are the most frequent, Southern winds are the hottest.
* **Bimodal Temperature Density:** The distribution of temperatures heavily skewing towards extreme heat (>30°C) exclusively when the `coco_label` is "Clear" or "Fair".

---

# Possible correlations

* A massive negative correlation (-0.83) between Air Temperature and Relative Humidity, indicating that the extreme heatwave was a "dry heat" event.
* A strong logical correlation between high atmospheric pressure (`pres` > 1020 hPa) and the absence of cloud cover, enabling maximum solar radiation.

---

# Hypotheses

What do you expect to discover? (Validated during EDA)

* **Hypothesis 1 (The Pressure Dome):** I expect to show that the absolute highest temperature peaks (>30°C) did not happen randomly, but were strictly triggered by a blocking high-pressure system that cleared the sky and allowed uninterrupted solar heating.
* **Hypothesis 2 (The Thermal Pump):** I expect to discover that while Katowice is generally cooled by prevailing Westerly Atlantic winds, the extreme heat anomaly was physically "imported" by rare Southerly and South-Easterly winds.
* **Hypothesis 3 (Dry Heat):** I hypothesize that rainy or heavily clouded days physically cap the temperature at around 22-25°C, whereas the clear-sky heatwave was characterized by plummeting relative humidity, making it a severe dry-heat event.
