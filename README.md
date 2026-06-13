# Getting Your Fare Share: Data-Driven Strategy for NYC Yellow Cab Drivers

A customer/operations analytics project translating 62,316 NYC yellow cab trip records (Feb 2026) into actionable, evidence-based recommendations for driver positioning, timing, and trip selection.

> University of Groningen — MSc Marketing Analytics and Data Science | Customer Models course project

## Business Questions

1. **What Drives Tipping?** — What determines whether a passenger tips, and how large the tip is as a share of the fare?
2. **The Morning Launch** — Where should a driver start a morning shift (05:00–10:00) to maximise the chance of a high-efficiency first trip?
3. **The Turnover Trap** — After a drop-off, how long should a driver wait for the next fare before relocating?

## Approach

| Challenge | Outcome | Model |
|---|---|---|
| Tipping behaviour | Tip incidence + tip % of fare | Two-part **Hurdle model** (Logit + Gamma GLM), validated against Tobit via Cragg's LR test |
| Morning zone selection | Binary success (fare/min ≥ median) | **Logistic Regression**, AUC = 0.79 |
| Wait-or-relocate decision | Time to next pickup | **Cox Proportional Hazards** model, with Weibull AFT as a parametric cross-check |

All models use cluster-robust standard errors at the pickup-zone level. Variable selection was guided by VIF screening (all retained variables VIF < 2.5).

## Key Findings

- **Tipping is near-universal among card riders (95.5%)**, so the real signal is in tip *size*, not whether a tip occurs. Tip % falls as fare size rises (anchoring effect), while toll/airport routes attract the highest tip percentages.
- **Starting a shift at 06:00 instead of 08:00** gives drivers a ~20 percentage point structural advantage in landing a high-efficiency first trip.
- **Drop-off location dominates wait time**: an outer-borough drop-off cuts the chance of a quick next pickup by ~80% (waits ~5x longer); a Queens drop-off means ~73% longer waits.
- **Cross-challenge synthesis** reveals no zone is uniformly best — airports (JFK, LaGuardia) top morning-success scores but rank lowest on tipping and pickup speed, while residential Upper Manhattan zones (Upper West Side North/South, Yorkville West) offer the best overall balance of tipping, efficiency, and flexibility.

## Data

Source: [NYC TLC Trip Record Data](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page), enriched with TLC taxi zone demographics and hourly weather data. Raw data is not included in this repository due to size; see the notebook for loading instructions.

## Tech Stack

Python · pandas · statsmodels · scikit-learn · lifelines · matplotlib / seaborn

## Notes & Limitations

This is an observational study — all findings represent associations, not causal effects, and should be read as defensible operating heuristics. Tipping analysis is restricted to credit-card trips (88.3% of the sample). The data cover a single winter month, so snowfall effects are period-specific.


