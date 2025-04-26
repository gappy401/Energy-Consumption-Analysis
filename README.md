
## 1. Introduction

This project focuses on understanding energy consumption patterns and investigating their relationship with temperature variations, particularly in July. The objectives are as follows:
1. Identify factors influencing energy consumption.
2. Analyze energy consumption variation with temperature increases in July.
3. Pinpoint significant determinants impacting energy usage.
4. Offer practical recommendations for energy conservation.
5. Demonstrate the effectiveness of energy reduction strategies using predictive modeling.

The project was conducted primarily using **R**, which facilitated data cleaning, exploratory analysis, feature engineering, and predictive modeling. R’s comprehensive libraries were critical for implementing statistical techniques, visualization, and model evaluation.

The dataset used is private and contains detailed information about residential energy consumption and weather conditions. For confidentiality, only the final processed dataset used for analysis is included in the `data/` folder, ensuring reproducibility while maintaining data privacy.

## 2. Exploratory Data Analysis (EDA)

### Dataset Overview
- **Static Housing Dataset**: 5,710 rows and 171 columns, with 8 numeric columns and 163 categorical ones. Each row is unique based on building ID.
- Key Variables: 
  - `building_id`: Unique identifier for each property.
  - `in.sqft`: House size in square feet.
  - `in.pv_system_size`: Solar panel size.
  - Other features related to infrastructure, insulation, and energy systems.

### Descriptive Analysis
- **Numerical Columns**: Variables like number of bedrooms and house size displayed roughly normal distributions.
- **Discrete Columns**: Regional Energy Deployment Type (categories: 95 and 96) and number of stories in a building (values: 1, 2, 3) showed right-skewed distributions.

### Correlation Analysis
A correlation matrix revealed significant associations between weather-related variables and energy consumption. These findings guided feature selection for the model.

### Data Cleaning
- Removed rows with only one unique value, reducing columns from 171 to 93.
- Retained columns with less than 5% blanks.
- Identified uneven distribution of buildings by county; Greenville had the highest density, followed by Colleton and Georgetown.

### Energy Consumption Dataset
- **Hourly Data**: Data for each building recorded hourly for all months of 2018; July 2018 was selected for analysis.
- Aggregated hourly energy consumption for July across all buildings, resulting in 130k rows and 137 variables.
- Addressed negative energy values caused by surplus solar energy (`in.pv` variables).
- Found strong positive correlations between energy usage and variables like number of bedrooms and building size.

### Weather Data Integration
- Weather data averaged for July, including temperature, humidity, wind, and radiation variables.
- Merged with energy consumption data to create the final dataset with 130k rows and 102 variables.

### Feature Engineering
Feature engineering was crucial in preparing and refining the dataset for predictive modeling:
1. Visualized mean energy consumption for categorical variables using bar graphs.
2. Investigated potential correlations using academic literature.
3. Used linear regression to test statistical significance of variables.

Key findings included the identification of variables such as infiltration rates, which displayed unexpected correlations, and significant weather-related variables that justified their inclusion in the modeling phase.

## 3. Modelling

The modeling phase involved iterative testing, training, and evaluation using linear regression, Gradient Boosting, and XGBoost models.

### Linear Regression
Linear regression revealed overfitting when incorporating numerous variables, with adjusted R-squared peaking at 69%. It was ultimately deemed unsuitable for this dataset.

### Gradient Boosting
Gradient Boosting improved predictive accuracy by capturing non-linear relationships and handling outliers effectively. However, there was still room for improvement in RMSE and R-squared values.

### XGBoost (Extreme Gradient Boosting)
XGBoost was selected as the final model due to its ability to address overfitting, handle complex relationships, and provide feature importance scores. It achieved:
- **RMSE**: ~6.31, the lowest among models.
- **R-squared**: ~91.9%, indicating strong explanatory power.

## 4. Energy Prediction at Warmer Temperatures

Using the XGBoost model, predictions were made for a 5°C increase in temperature across South Carolina counties. Key findings:
- Greenville exhibited the highest energy consumption, with Horry experiencing the largest percentage increase (33%).
- Hourly energy consumption peaked around 4 PM, and overall usage increased in magnitude without a change in pattern.

These findings underscore the impact of minor temperature variations on energy demand and emphasize the need for strategic energy management.

## 5. Actionable Energy Efficiency Strategies

To address rising energy consumption, the following strategies were proposed:
- Improve ceiling fan efficiency, hot water fixtures, and ACH levels, though these achieved minimal reductions.
- Focus on installing "1KwDC" Solar Panel Systems in buildings without existing solar setups, offering significant energy savings through a cost-efficient and feasible approach.

## 6. Conclusion

The analysis concluded that installing '1KwDC' solar panels is the most cost-effective energy efficiency strategy, achieving a 28% reduction in energy consumption. This strategy outperformed alternatives like insulation upgrades or appliance enhancements, which often require higher costs and extensive modifications.

## Data and Code Distribution/Reproducibility

The final processed dataset used for this project is available in the `data/` folder. This dataset represents the cleaned and aggregated data prepared for analysis. All analysis was performed using **R**. 

Please note that the code developed for this project is **not open for distribution**. It remains proprietary and is not included in this repository. However, the provided dataset and findings ensure reproducibility of the analysis and conclusions.

