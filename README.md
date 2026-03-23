# Urban Mobility Intelligence: Uber Hotspot & Demand Analysis

**Project Overview:**  
Analyzed Uber pickup data in New York City to uncover ride demand patterns, identify geographic hotspots, and predict high-demand periods using machine learning. The goal was to generate actionable insights for operational planning, including driver allocation and dynamic pricing.

---

## Objectives

- Explore temporal patterns in ride demand
- Identify peak hours and high-demand days
- Detect geographic hotspots using clustering
- Build a predictive model for high-demand rides
- Derive practical business insights for driver allocation and pricing

---

## Day 1 – Data Loading & Cleaning

- Loaded Uber ride data and inspected for missing or inconsistent values
- Converted `Date/Time` into datetime format
- Extracted time-based features: `hour`, `day`, `weekday`
- Created `is_weekend` feature to distinguish weekday vs weekend patterns
- Applied **KMeans clustering** on latitude and longitude to define `zone` feature for geographic hotspots
- Explored data distributions through histograms and scatter plots to identify trends and anomalies

**Key Takeaway:** Cleaning and feature engineering early helped clarify both temporal and geographic patterns for downstream analysis.

---

## Day 2 – Temporal Analysis

- Added a `demand` flag for high-demand rides (focused on **4–7 PM**, the typical evening commute)
- Analyzed ride volume by hour, weekday, and weekend
- Visualized:
  - Hourly ride distribution
  - Weekday vs weekend patterns
  - Heatmap of hour vs weekday

**Insights:**  
- Weekdays show sharp spikes around commute hours  
- Weekends have flatter ride distributions throughout the day  
- Evening demand consistently peaks, highlighting critical operational windows

---

## Day 3 – Geographic Hotspots

- Created geographic heatmaps using latitude and longitude to visualize ride density
- Defined clusters (`zone`) to identify high-demand neighborhoods
- Used **Folium** to map 5,000 sample rides, balancing performance and hotspot visibility
- Highlighted areas with consistently high evening demand (e.g., Midtown, Financial District)

**Business Insight:** Drivers can be pre-positioned in these hotspots during peak hours to reduce wait times and improve service.

---

## Day 4 – Feature Engineering & ML Prep

- Selected predictive features: `hour`, `weekday`, `is_weekend`, `zone`
- Split dataset into training and test sets
- Ensured target variable (`demand`) correctly reflected high-demand periods
- Checked for class imbalance and missing values

**Rationale:** Carefully engineered features and clean data ensured the model could capture real-world patterns accurately.

---

## Day 5 – Modeling & Evaluation

- Trained a **Random Forest Classifier** to predict high-demand rides
- Evaluated using confusion matrix and classification report
- Analyzed **feature importance**, revealing:
  - Hour, zone, and weekday as top predictors
- Compared predicted vs actual high-demand periods to validate model performance

**Takeaways:**  
- Random Forest captured non-linear demand patterns that simpler models missed  
- Predicted high-demand windows aligned closely with observed peak times  
- Supports operational planning like surge pricing and dynamic driver allocation

---

## Day 6 – Business Insights & Visualization

- Mapped predicted high-demand zones on NYC map to highlight top hotspots
- Actionable recommendations:
  - Increase driver presence during **4–7 PM** on weekdays
  - Adjust pricing dynamically in high-demand zones
  - Monitor hotspots for real-time resource allocation
- Visualized results through heatmaps and feature importance charts for stakeholder communication

---

## Optional Enhancements / Recruiter Highlights

- Interactive **Folium maps** showing predicted demand hotspots
- Feature importance chart illustrating top predictors (hour, zone, weekday)
- A small function `predict_demand` to simulate whether a ride at a specific hour/location would be high-demand
- End-to-end workflow from **EDA → Feature Engineering → Modeling → Prediction → Business Insights**, demonstrating hands-on ML project experience

**Why this stands out:** Combines technical skills, data visualization, and actionable business insights in a real-world context. Demonstrates not just modeling, but thoughtful problem-solving aligned with operational decisions.
