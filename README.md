Urban-Mobility-Intelligence-Uber-Analysis
Uber Hotspot Detection & Demand Prediction

Analyzed Uber pickup data in NYC using Python to uncover temporal and spatial demand patterns, detect high-density zones, and predict ride demand using machine learning.

Objectives
Analyze ride demand over time (hour, weekday, weekend)
Identify peak periods and high-demand days
Detect geographic hotspots using clustering
Build ML models to predict ride demand
Generate actionable business insights for operational decisions
Day 1 – Data Loading & Cleaning

Tasks:

Loaded Uber April 2014 dataset.
Inspected and cleaned data.
Converted Date/Time column to datetime.
Created initial features: hour, day, weekday, month.
Performed basic exploratory data analysis (EDA).

Observations:

Dataset contains 564,516 rows with 4 columns: Date/Time, Lat, Lon, Base.
No missing values; Lat and Lon capture geolocation; Base indicates Uber dispatch base.
Day 2 – Temporal Analysis & EDA

Tasks:

Created time-based features: hour, weekday, is_weekend, time_bucket.
Analyzed ride demand by hour and weekday.
Built visualizations:
Rides per hour
Rides per weekday
Heatmaps of rides (hour vs weekday)

Insights:

Hour-wise demand:
Morning peak: 8–10 AM
Evening peak: 4–7 PM
Late-night increase: 11 PM–1 AM
Lowest demand: 0–6 AM
Weekday patterns:
Weekdays show strong commute spikes, especially Wednesday.
Weekends have evenly distributed demand; Saturday evenings are busiest.
Mondays and Sunday nights have lower activity.
Time buckets: Night, Morning, Afternoon, Evening – Evening consistently high demand.
Day 3 – Spatial Analysis & Base Study

Tasks:

Applied KMeans clustering on Lat and Lon to create zone feature.
Plotted Uber pickup density using Folium maps.
Analyzed demand by Uber Base.

Insights:

Zones capture geographical demand hotspots (commercial areas, transit hubs, nightlife districts).
Base B02682 and B02512 are most active, useful for driver allocation.
Heatmaps show concentrated high-demand regions, especially during commute hours.
Day 4 – Feature Engineering & Target Creation

Tasks:

Added features for ML: hour, weekday, is_weekend, zone.
Created target variable demand to indicate high-demand periods (4–7 PM).
Split data into train/test sets for modeling.

Observations:

Peak hours correctly labeled for evening commute, but analysis shows other peaks exist (morning, late-night).
Features now capture temporal (hour, weekday, weekend) and spatial (zone) patterns.
Day 5 – Model Training & Evaluation

Tasks:

Trained models:
Linear Regression (baseline)
Random Forest Regressor/Classifier

Results:

Linear Regression performed poorly due to limited hourly data points.
Random Forest significantly outperformed Linear Regression, capturing non-linear patterns.
Feature importance analysis: hour, zone, and weekday are key predictors; is_weekend contributes moderately.

Insights:

Random Forest accurately predicts high-demand periods.
Model captures temporal and spatial variations effectively.
Visualizations show strong alignment between actual vs predicted ride counts.
Day 6 – Business Insights & Applications

Applications:

Driver allocation: Increase availability during morning and evening peaks.
Dynamic pricing: Adjust fares for high-demand periods and zones.
High-demand zone identification: Deploy resources in clusters with more pickups.
Weekend planning: Even distribution of drivers due to flatter demand.
Late-night monitoring: Improve service availability in niche areas.

Optional Enhancements / Recruiter Highlights

Interactive Folium maps for hotspots visualization
Feature importance chart for top predictors (hour, zone, weekday)
Single-ride prediction function (predict_demand) for business simulations
Clear ML workflow from EDA → Feature Engineering → Modeling → Insights
Final Summary

This project demonstrates the practical application of feature engineering, spatial-temporal analysis, and advanced machine learning to predict Uber demand in NYC.

Random Forest models successfully captured complex non-linear patterns.
High-demand periods can be predicted across morning, evening, and late-night hours.
Zones derived from clustering highlight geographic hotspots.
Provides actionable insights for driver allocation, surge pricing, and operational optimization.
