# NYC Subway On-Time Performance

## TL;DR
Using 2025 MTA terminal performance data and monthly weather data, I modeled subway on-time performance as a function of line, weekday vs weekend operations, and precipitation. Weekday congestion and structural line differences explain more variation in performance than weather alone. The N line emerges as a high-volume, below-average performer — making it a high-impact operational intervention target.


## Business Question
Which operational and environmental factors (time of day, line, station, weather, and delay propagation) most strongly predict subway delays during peak hours, and where should the MTA prioritize intervention to reduce total system-wide delay minutes?

## Dataset

Primary dataset:
- MTA Terminal On-Time Performance (2025)  
  Source: data.ny.gov (Terminal-level monthly OTP by line and day type)

Weather data:
- NOAA monthly precipitation data for NYC (via Meteostat Python package)

Structure:
- Each row represents a line × month × day_type combination
- Metrics include:
  - num_on_time_trips
  - num_sched_trips
  - terminal_on_time_performance


## Method
- Data cleaning: Merge trip-level performance data with station and weather data
- EDA: Compute on-time rates, average delay minutes, and peak/off-peak comparisons
- Modeling (if applicable): Logistic regression or gradient boosting to estimate probability of delay

## Key Insights

1. Weekday operational pressure materially reduces on-time performance.  
   Across major lines (N, B, 2, A), predicted on-time probability drops by ~2.5–3.5 percentage points on weekdays relative to weekends, holding precipitation constant.

2. Structural line differences persist after controlling for weather and day type.  
   The N, B, and 2 lines show significantly lower baseline on-time probabilities compared with higher-performing lines such as A, L, and 7, suggesting infrastructure or operational complexity differences.

3. Weather has a statistically significant but modest effect.  
   Monthly precipitation is statistically significant, but the effect size is small relative to weekday load and line-level differences. Operational congestion appears more impactful than weather alone.

4. The N line represents a high-impact intervention target.  
   It combines high scheduled volume with below-average on-time performance, placing it in the high-volume / low-performance quadrant—maximizing system-wide delay reduction potential if improved.


## Skills Demonstrated
- Python
- Pandas
- Data cleaning & feature engineering
- Visualization (Matplotlib / Seaborn / Plotly)
- Statistical reasoning
- Business interpretation

## Modeling Approach
- Aggregated line-level trip counts by month and day type.
- Fit a binomial logistic regression:
  - Target: (num_on_time_trips, late_trips)
  - Predictors: line (categorical), day_type, monthly precipitation
- Used predicted probabilities to quantify weekday vs weekend performance differences while holding precipitation constant.

## Reproducibility
Instructions to reproduce:
1. Download raw datasets into the `/data` folder
2. Run `analysis.ipynb`
3. Outputs will be generated in `/outputs`
