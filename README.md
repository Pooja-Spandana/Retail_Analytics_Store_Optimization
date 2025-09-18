# ***Integrated Retail Analytics for Store Optimization and Demand Forecasting***

## ***Project Objective***
This project applies **machine learning and data analytics** to optimize retail performance by:
1. Detecting and handling anomalies in sales data.
2. Forecasting demand at **Store × Department level**.
3. Enhancing customer experience via **segmentation and personalized marketing strategies**.

---

## ***Workflow Overview***

### *1. Data Cleaning & Preprocessing*
- Explored all 3 datasets and merged them into a single dataframe
- Handled missing values in markdown and economic indicators.
- Clipped extreme outliers (`Weekly_Sales_clipped`) while retaining true anomalies for business insights.

### *2. Anomaly Detection*
- **IQR-based detection** (`anomaly_iqr`) and **time-series based detection** (`anomaly_ts`).
- Overlayed holiday weeks on sales trends to capture seasonal effects.
- **Decision:** Kept anomalies since they represent true events (holidays, promotions, economic shocks).

### *3. Feature Engineering*
- **Time-based:** Year, Month, Quarter, WeekOfYear, DayOfWeek.
- **Lag features:** `Sales_Lag1`, `Sales_Lag2`.
- **Moving averages:** `Sales_MA3`, `Sales_MA6`.
- **Holiday indicators:** `IsHoliday`, `IsHoliday_NextWeek`.
- **Markdown features:** `Total_MarkDown`, `Has_MarkDown`.
- **Store-related:** `Size_Category`, `Sales_per_sqft`.

### *4. Exploratory Data Analysis (EDA)*
- Sales distribution by holiday, store type, and store size.
- Sales distribution across Time.
- Holiday effect overlay on sales trends.
- Performed univariate, bivariate & multivariate analysis. 
- Insights on seasonal and promotion-driven fluctuations.

### *5. Customer Segmentation (Store & Department)*
- Aggregated features at **Store** and **Dept** levels.
- Applied **KMeans clustering** with Elbow & Silhouette evaluation.
- External validation via **Homogeneity & Completeness** against Store Type.
- Profiles & business insights for each cluster:
  - **Stores:** growth anchors, markdown-driven, steady, niche formats.
  - **Departments:** star categories, balanced performers, markdown-heavy clearance depts.

### *6. Market Basket Analysis (MBA)*
- Association rules mined at **department level**.
- Top rules table with **support, confidence, lift**.
- **Scatterplot:** Support vs Confidence (colored by Lift).
- **Network graph:** Department co-purchase clusters and hub depts.
- Business insights:
  - Dept 49 & 98 = central cross-sell hubs.
  - Strong pairs/clusters for bundling, store layout, recommendations, and inventory planning.

### *7. Demand Forecasting - Modeling Approach*
The modeling process was conducted in two stages:

1. **Global Model Comparison**
   - Multiple algorithms were tested on the full dataset, including:
     - Baseline models (Naïve)
     - Time-series models (Prophet, SARIMA)
     - Tree-based models (LightGBM, Random Forest, XGBoost)
     - Deep Learning (LSTM)
   - Models were evaluated using RMSE, MAE, and MAPE.
   - **XGBoost emerged as the best-performing model**, consistently outperforming baselines and tree-based alternatives.

2. **Scaling Across Store × Dept**
   - Instead of repeating the model comparison for every Store × Dept, we selected XGBoost as the final model and trained it per group.
   - Each Store × Dept received its own trained XGBoost model, allowing the algorithm to capture localized demand dynamics while maintaining global consistency.
   - Evaluation metrics (MAE, RMSE, MAPE) were stored per group in `results_df`, and models were saved for generating **4-week forecasts**.
   - Results stored in clean DataFrame for **Store × Dept-level forecasts** (purchase order granularity)

### *8. Personalized Marketing & Inventory Strategies*
- **Stores:**
  - High performers → expand premium products, loyalty programs.
  - Markdown-driven → optimize promotion ROI.
  - Stable → efficient replenishment.
  - Niche/express → SKU rationalization & local targeting.
- **Departments:**
  - Stars → prioritize inventory, cross-sell.
  - Balanced → sustain with steady markdowns.
  - Markdown-heavy/low sales → clearance campaigns & SKU rationalization.

---

## ***Key Business Takeaways***
- Retaining anomalies is essential since they reflect **true demand shocks**.
- Clustering revealed **hidden behavioral patterns** beyond Store Type (A/B/C).
- Dept 49 & 98 emerged as **cross-selling anchors** for promotions & recommendations.
- Demand forecasting enables **4-week ahead planning**, supporting **purchase orders** at Store × Dept level.
- Personalized marketing & inventory strategies can significantly enhance **profitability and customer experience**.

---

## ***Outputs***
- `FE_Dataset` → Featured Engineered, clean dataset used for modeling.
- `future_forecasts_4weeks` → Clean DataFrame with 4-week forecasts.

---

## ***Conclusion***
- This project demonstrates how integrating anomaly detection, segmentation, market basket analysis, and forecasting creates a **comprehensive retail analytics framework**.  
- By leveraging XGBoost for localized demand forecasting and clustering for strategic insights, the solution provides actionable guidance for **inventory planning, promotional optimization, and customer personalization**.  
- The approach ensures that business decisions are **data-driven, scalable, and directly aligned with profitability and customer experience goals**.  