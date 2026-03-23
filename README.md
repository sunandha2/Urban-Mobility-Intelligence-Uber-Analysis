# Urban-Mobility-Intelligence: Uber Analysis

**Uber Hotspot Detection & Demand Prediction**  
Analyzed Uber pickup data using Python to uncover temporal and geographic demand patterns, detect peak hours, and predict high-demand zones using machine learning.

---

## Objectives

- Analyze temporal patterns in Uber demand  
- Identify peak hours and high-demand days  
- Detect geographic hotspots using clustering  
- Build a machine learning model to predict high-demand rides  
- Generate actionable business insights for decision-making  

---

## Day 1 – Data Loading & Cleaning

- Loaded Uber ride data and inspected for missing values  
- Converted `Date/Time` to datetime format  
- Extracted time-based features: `hour`, `day`, `weekday`  
- Created `is_weekend` feature to distinguish weekday vs weekend patterns  
- Applied KMeans clustering on latitude and longitude to define `zone` feature for geographic hotspots  
- Performed basic EDA and visualizations to understand data distributions  

---

## Day 2 – Time-Based Analysis

- Created `demand` column to identify **high-demand rides** (4–7 PM)  
- Analyzed ride demand by hour, weekday, and weekend indicator  
- Visualized:
  - Rides per hour  
  - Rides per weekday  
  - Hour vs weekday heatmap  
- **Key Insights**:
  - Peak demand occurs during **4 PM – 7 PM**  
  - Weekdays show **sharp commute-based spikes**  
  - Weekends have **more evenly distributed demand**  
  - Evening hours consistently show high ride activity  

---

## Day 3 – Geographic Analysis & Heatmaps

- Generated geographic heatmaps for ride density using latitude & longitude  
- Created cluster-based `zone` feature to identify high-demand hotspots  
- Visualized high-demand rides on NYC map using Folium heatmaps (sample 5,000 rides for performance)  
- Derived business insights for **driver allocation in high-density zones**  

---

## Day 4 – Feature Engineering & ML Preparation

- Selected features: `hour`, `weekday`, `is_weekend`, `zone`  
- Split data into **train and test sets**  
- Ensured target variable (`demand`) is correctly defined for classification  
- Confirmed data readiness for machine learning  

---

## Day 5 – Model Training & Evaluation

- Trained **Random Forest Classifier** to predict high-demand rides  
- Evaluated model performance using classification report and confusion matrix  
- Observed **feature importance**:
  - Hour, zone, and weekday are top predictors  
- Compared predicted vs actual high-demand periods  

**Key Insights**:

- Random Forest captures **non-linear demand patterns** that simple models cannot  
- Model can predict **peak periods (4–7 PM) and high-demand zones**  
- Enables **operational planning** like surge pricing and driver allocation  

---

## Day 6 – Business Insights & Visualization

- Visualized predicted high-demand zones on NYC map  
- Highlighted top zones during peak hours for targeted interventions  
- Generated actionable business insights:
  - Increase drivers during **4–7 PM**  
  - Adjust pricing strategies in **high-demand zones**  
  - Monitor hotspots for dynamic resource allocation  
- Summarized project findings and applicability for urban mobility optimization  

---

## Key Highlights & Recruiter-Friendly Features

- **Interactive Folium maps** to visualize predicted demand hotspots  
- **Feature importance chart** showing top predictors (hour, zone, weekday)  
- **Single-ride prediction function (`predict_demand`)** for business simulations and “what-if” scenarios  
- Clear **end-to-end ML workflow**: EDA → Feature Engineering → Modeling → Prediction → Business Insights  
