# Operational Reliability Under Peak Load  
### A Systems Analytics Case Study Using NYC Subway Data

## Executive Summary

This project models how operational systems degrade under load and identifies high-impact intervention targets using real-world performance data.

Using NYC subway terminal on-time performance data as a proxy for a large-scale operational system, I:

- Quantified reliability differences across structural units (lines)
- Measured weekday congestion effects
- Assessed external shock impact (precipitation)
- Built a binomial logistic regression model to estimate delay probability
- Identified high-volume, low-performance segments with the greatest leverage for improvement

📄 Executive Summary Slides: outputs/NYC_Subway_OTP_Executive_Summary.pdf

The analysis demonstrates how statistical modeling can prioritize interventions that reduce total system-wide failure exposure under peak operational pressure.

---

## Business Framing

Large operational systems (transit networks, payment processors, cloud platforms, supply chains) experience performance degradation under load.

Core question:

When volume increases and external conditions vary, which structural components of the system create the largest reliability risk — and where should intervention resources be allocated to maximize impact?

This case study treats subway on-time performance as a reliability system under stress.

The objective is not transit optimization — it is operational decision modeling.

---

## Dataset

Primary:
- MTA Terminal On-Time Performance (monthly, by line and day type)

External Feature:
- NOAA precipitation data for NYC (via Meteostat)

Unit of Analysis:
- Line × Month × Day Type (Weekday vs Weekend)

Observations: 540 aggregated records

---

## Feature Engineering

- Converted scheduled and on-time trip counts into binomial success/failure pairs
- Created late_trips = num_sched_trips - num_on_time_trips
- Encoded line as categorical structural unit
- Encoded weekday vs weekend (day_type)
- Aggregated monthly precipitation totals

---

## Modeling Approach

Model: Binomial Logistic Regression

Target:
(num_on_time_trips, late_trips)

Predictors:
- Line (categorical)
- Day type (weekday vs weekend)
- Monthly precipitation

Interpretation:
Coefficients estimate log-odds change in on-time probability relative to baseline.

---

## Key Findings
# Operational Reliability Under Peak Load  
### A Systems Analytics Case Study Using NYC Subway Data

## Executive Summary

This project models how operational systems degrade under load and identifies high-impact intervention targets using real-world performance data.

Using NYC subway terminal on-time performance data as a proxy for a large-scale operational system, I:

- Quantified reliability differences across structural units (lines)
- Measured weekday congestion effects
- Assessed external shock impact (precipitation)
- Built a binomial logistic regression model to estimate delay probability
- Identified high-volume, low-performance segments with the greatest leverage for improvement

📄 Executive Summary Slides: outputs/NYC_Subway_OTP_Executive_Summary.pdf

The analysis demonstrates how statistical modeling can prioritize interventions that reduce total system-wide failure exposure under peak operational pressure.

---

## Business Framing

Large operational systems (transit networks, payment processors, cloud platforms, supply chains) experience performance degradation under load.

Core question:

When volume increases and external conditions vary, which structural components of the system create the largest reliability risk — and where should intervention resources be allocated to maximize impact?

This case study treats subway on-time performance as a reliability system under stress.

The objective is not transit optimization — it is operational decision modeling.

---

## Dataset

Primary:
- MTA Terminal On-Time Performance (monthly, by line and day type)

External Feature:
- NOAA precipitation data for NYC (via Meteostat)

Unit of Analysis:
- Line × Month × Day Type (Weekday vs Weekend)

Observations: 540 aggregated records

---

## Feature Engineering

- Converted scheduled and on-time trip counts into binomial success/failure pairs
- Created late_trips = num_sched_trips - num_on_time_trips
- Encoded line as categorical structural unit
- Encoded weekday vs weekend (day_type)
- Aggregated monthly precipitation totals

---

## Modeling Approach

Model: Binomial Logistic Regression

Target:
(num_on_time_trips, late_trips)

Predictors:
- Line (categorical)
- Day type (weekday vs weekend)
- Monthly precipitation

Interpretation:
Coefficients estimate log-odds change in on-time probability relative to baseline.

---

## Key Findings

### Load Pressure Effect

Weekdays show a statistically significant decrease in on-time probability relative to weekends.

Across major lines:
- Weekday on-time probability drops by ~2.5–3.5 percentage points
- Weekday trips account for over 2.1 million scheduled trips vs ~630k on weekends

Operational congestion has a materially larger impact than weather.

---

### Structural Risk Differences Persist

After controlling for weather and day type:

- N, B, and 2 lines show significantly lower baseline reliability
- A, L, and 7 lines show structurally higher reliability

---

### Weather Is Secondary

Monthly precipitation is statistically significant but economically small.

Operational stress dominates environmental effects.

---

### High-Leverage Intervention Target

The N line combines high scheduled volume with below-average reliability, placing it in the high-volume / low-performance quadrant.

Improving this line would reduce system-wide failure exposure disproportionately.

---

## What This Demonstrates

- Structured reliability modeling
- Proper grouped binomial regression
- Business interpretation of coefficients
- Separation of statistical vs operational significance
- Executive-level decision framing

---

## Reproducibility

1. Place raw datasets in `/data`
2. Run `notebooks/analysis_clean.ipynb`
3. Outputs will be generated in `/outputs`

