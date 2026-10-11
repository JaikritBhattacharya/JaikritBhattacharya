# Jaikrit Bhattacharya

### Quantitative Finance · Golf Analytics · Applied Data Science

I build explainable models and decision tools from messy, multi-source data—financial cash flows, fund data, weather records, sensor telemetry, and environmental time series.

My work is organized around three themes:

- **Quantitative finance:** ranking, scenario analysis, fees, risk, and investment decision support
- **Golf analytics:** combining golf-domain knowledge with climate, geospatial, and performance data
- **Applied data science:** data quality, regression, time-series analysis, forecasting, and visualization

## Featured work

### Quantitative finance

#### [Private Markets Fund Comparison](https://fundperformanceframework.streamlit.app/)

An interactive decision framework for comparing private-market funds using dated cash flows, XIRR, investment multiples, fee analysis, deterministic scenarios, paired Monte Carlo simulation, and formula-linked Excel checks. It focuses on how assumptions about timing, fees, and terminal value change the decision—not on predicting returns.

#### [Mutual Fund Ranking Pipeline](https://github.com/JaikritBhattacharya/mutual-fund-ranking-pipeline)

A tested Python engine that screens funds for eligibility, ranks them within peer groups using rolling-return and Sharpe-ratio percentile scores, handles ties, and records why a fund was excluded. The public version uses synthetic data.

### Golf analytics

#### [Golf Courses, Climate, and Water-Use Signals](https://github.com/JaikritBhattacharya/golf-course-water-signals)

An alternative-data study combining evapotranspiration, NOAA weather, land-cover comparisons, and two very different climates to examine golf-course water-demand signals. The analysis treats ET as a useful proxy—not as measured irrigation—and keeps that limitation visible.

### Applied data science

#### [Regression and Time-Series Forecasting](https://github.com/JaikritBhattacharya/regression-time-series-forecasting)

An R project covering transformations, regression diagnostics, model selection, seasonal decomposition, autoregressive models, and forecast intervals.

#### [Environmental Sensor Quality Control](https://github.com/JaikritBhattacharya/environmental-sensor-quality-control)

An R workflow that checks timestamps, sensor state, physical bounds, battery levels, and missingness before the data reaches a model or chart.

#### [Flood-Stage Monitoring](https://github.com/JaikritBhattacharya/flood-stage-monitoring)

An R analysis that joins river-gauge observations to site-specific thresholds, identifies first crossings, and measures major-stage exceedance.

## More projects

- [Climate, emissions, and space-data visualization](https://github.com/JaikritBhattacharya/climate-emissions-visualization)
- [Quantitative analysis portfolio and full project index](https://github.com/JaikritBhattacharya/quantitative-analysis-portfolio)
- [Introductory Python course projects](https://github.com/JaikritBhattacharya/intro-python-course-projects)

## How I work

- Check the data before trusting the model.
- Use comparison groups and independent sources when one dataset is not enough.
- Keep assumptions, exclusions, and limitations visible.
- Prefer methods I can explain, test, and audit.
- Label exploratory results honestly instead of presenting them as causal.
