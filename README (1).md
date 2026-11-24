# FMCG Demand Forecasting

## Overview
This project forecasts how many units of each product a supermarket-type business will sell over the next 7 days. Using three years of daily sales data from 7 European countries, the model helps planners decide how much stock to keep, so they run out less often and hold less extra inventory.

## Project Workflow
1. **Data Collection & Cleaning**
   - Loaded the dataset (about 1.1 million rows, 33 columns, 102 products, 13 stores, 2021-2023).
   - Checked for missing values, duplicate rows, strange labels and impossible values. The data was already quite clean.
   - Noticed that on days when a product is out of stock, sales drop from about 61 to 12 units, so recorded sales understate real demand.

2. **Exploratory Data Analysis (EDA)**
   - Visualized sales patterns using **Matplotlib and Seaborn**.
   - Found that weekends sell about **20% more** than weekdays and that summer is busier.
   - Grouped products with **ABC analysis**: 49 products ("A" products) bring in about 79% of revenue.
   - Checked correlations and ran simple statistical tests. Promotions and weekends increase sales, while weather and supplier lead time have almost no effect.
   - Found that promotions raise sales by about **91%**.

3. **Feature Engineering & Model Training**
   - Created features such as sales from 7, 14 and 21 days ago, recent averages, weekday, month and promotion information.
   - Split the data by time, not randomly: trained on the past and tested on the **last 90 days** so the model never sees the future.
   - Compared simple baselines (same as 7 days ago, 28-day average) with **Linear Regression, Random Forest and Gradient Boosting**.
   - Picked the final model (**Gradient Boosting**) using time-series cross-validation, not the test data.

4. **Model Evaluation**
   - Used **MAE, RMSE, MAPE and WAPE** to measure forecast error.
   - Gradient Boosting made about **49% less error** than the simple "same as 7 days ago" rule (WAPE 15.5% vs 30.7%).
   - Checked that the model was fair across sales channels and looked at which features it relied on most.

5. **Business Impact**
   - Used the forecast errors to estimate **safety stock** (extra stock kept as a buffer): about **50% less** needed (11,862 down to 5,877 units for the 10 products tested).
   - Estimated that stockouts cost about **2.5% of revenue**.

6. **Improvements & Future Work**
   - Test on a longer period than 90 days, to cover more seasons.
   - Try other models like **LightGBM or XGBoost**.
   - Include more unstable products (all products in this data turned out to be fairly stable).
   - Check fairness again using real small-shop data.

## Technologies Used
- **Python** (Pandas, NumPy, Scikit-learn, SciPy, Matplotlib, Seaborn)
- **Machine Learning** (Linear Regression, Random Forest, Gradient Boosting, Forecast Error Metrics)
- **Jupyter Notebook** (Project Development)

## Results & Findings
- **Best model: Gradient Boosting**, with an average miss of about 29 units per product per channel per day, compared with 57 for the simple rule.
- Past sales (recent history) are what the model relies on most, followed by promotions.
- Promotions and weekends are the main drivers of demand; weather and lead time did not matter in this data.
- The model slightly **over-forecasts the small Convenience channel (+3.7%)** and has its highest error there, so that channel should be monitored.
- Better forecasts mean smaller safety stock, which could free up cash and reduce waste.

## Limitations
- The test period is only the last 90 days.
- Product prices are fixed, so price and promotion effects overlap.
- Promotions are assumed to be known in advance.
- The data may be simulated, since weather and lead time had no effect.

## Next Steps
- Try more advanced models and tune them further.
- Test the forecast on more time periods and more products.
- Build a simple dashboard to compare forecast and actual sales.
- Share the project on GitHub with a clear folder structure.
