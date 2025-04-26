# README

## 1. Introduction

This project focuses on understanding energy consumption patterns and investigating their relationship with temperature variations, particularly in July. The objectives are as follows:
1. Identify factors influencing energy consumption.
2. Analyze energy consumption variation with temperature increases in July.
3. Pinpoint significant determinants impacting energy usage.
4. Offer practical recommendations for energy conservation.
5. Demonstrate the effectiveness of energy reduction strategies using predictive modeling.

The project begins with Exploratory Data Analysis (EDA) and data cleaning, leading to the development of predictive models. The dataset includes:
- Information about individual residences, such as unique building IDs and property attributes.
- Hour-by-hour energy consumption data for each residence.
- Hourly weather data organized by geographic regions, serving as an external factor influencing energy patterns.

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
- **Discrete Columns**: Regional Energy Deployment Type (categories: 95 and 96) and number of stories in a building (values: 1, 2, 3) showed right-skewed distributions (see Fig. 2.1 and 2.3).

### Correlation Analysis
A correlation matrix revealed significant associations between weather-related variables and energy consumption. These findings guided feature selection for the model.

### Data Cleaning
- Removed rows with only one unique value, reducing columns from 171 to 93.
- Retained columns with less than 5% blanks.
- Identified uneven distribution of buildings by county; Greenville had the highest density, followed by Colleton, Georgetown, and others (see Fig. 2.5).

### Energy Consumption Dataset
- **Hourly Data**: Data for each building recorded hourly for all months of 2018; July 2018 was selected for analysis.
- Aggregated hourly energy consumption for July across all buildings, resulting in 130k rows and 137 variables.
- Addressed negative energy values caused by surplus solar energy (e.g., `in.pv` variables) (see Fig. 2.6).
- Found strong positive correlations between energy usage and variables like number of bedrooms and building size (see Fig. 2.7).
- Observed similar hourly energy consumption patterns across counties, differing in magnitude (see Fig. 2.8).

### Weather Data Integration
- Weather data averaged for July, including temperature, humidity, wind, and radiation variables.
- Merged with energy consumption data to create the final dataset with 130k rows and 102 variables.

### Feature Engineering
Feature engineering plays a pivotal role in preparing and refining the dataset for predictive modeling. It helps identify relevant features, reduce dimensionality, and prevent overfitting caused by irrelevant or incorrectly represented variables.

Steps undertaken:
1. Visualized mean energy consumption using bar graphs for categorical variables.
2. Investigated potential correlations between variables and energy usage using academic literature.
3. Applied linear regression to determine statistical significance for each variable.

Key Observations:
- A significant increase in average energy consumption for hot water fixtures during summer was unexpected, as they are typically used less during this period (see Fig. 3.0).
- Income showed a negligible correlation (~0.04), so it was excluded as a major factor.
- Infiltration exhibited an inverse relationship with energy consumption, revealing that higher ACH (air changes per hour) reduced air replacement frequency (see Fig. 3.1).

Using this process, 40 key variables were selected for modeling. Weather-related features demonstrated strong correlations with energy consumption, justifying their inclusion (see Fig. 3.2 and Fig. 3.3).

## 3. Modelling

### Linear Regression
Linear regression establishes a linear relationship between independent and dependent variables by minimizing the difference between observed and predicted values.

Key Insights:
- Testing up to 20 models revealed that adding more variables increased multiple R-squared but reduced adjusted R-squared, signaling overfitting.
- Adjusted R-squared peaked at 69%, indicating limited explanatory power. Linear regression was deemed unsuitable, prompting a transition to Gradient Boost methods.

### Gradient Boosting
Gradient Boosting is an ensemble method that combines decision trees sequentially, correcting errors from previous iterations to improve predictions.

Advantages:
- Captures complex non-linear relationships.
- Robust against outliers.
- Effortlessly handles numerical and categorical variables.
- Built-in regularization prevents overfitting.
- Feature importance scores identify key predictors.

Evaluation metrics (RMSE and R-squared) showed Gradient Boosting as a better fit than linear regression but left room for improvement.

### XGBoost (Extreme Gradient Boosting)
XGBoost is a scalable, efficient implementation of Gradient Boosting that leverages regularization, parallel computing, and tree pruning.

Results:
- RMSE: ~6.31, the lowest among models tested.
- R-squared: ~91.9%, indicating 91.9% of variability explained by independent variables.

XGBoost proved to be the optimal model due to its predictive power, accuracy, and robustness against complex data scenarios.

## 4. Energy Prediction at Warmer Temperatures

Using the final model, we predicted energy consumption across South Carolina counties for a 5°C temperature increase. Greenville exhibited the highest overall energy consumption, followed by Colleton.

Fig. 4.2  
This map aligns with prior consumption trends, indicating a general increase in magnitude rather than a shift in patterns. County-wise analysis revealed Horry had the highest percentage increase (33%), making it the most impacted by the temperature change.

Fig. 4.3  
Hourly energy consumption peaked at around 4 PM during July, correlating with temperature increases (see Fig. 4.4). Despite consistent patterns, a 5°C rise resulted in a notable 30% surge in usage, highlighting the substantial impact of minor temperature variations.

Strategies to address these surges:
- **Load-Shedding**: Schedule blackouts during peak demand to manage distribution efficiently.
- **Consumer Communication**: Encourage behavior adjustments during peak hours to alleviate grid strain.
- **Maintenance Scheduling**: Conduct power grid maintenance during low-demand periods to ensure reliability.

These findings emphasize the importance of effective energy management to address demand surges and plan for sustainable usage (see Fig. 4.5).

## 5. Actionable Energy Efficiency Strategies

Recent temperature-driven surges in energy consumption underscore the critical need for effective energy efficiency strategies. These include:
- Addressing apparent variables like ceiling fan efficiency, hot water fixtures, and ACH levels, though these achieved only a minimal 1% reduction (Fig. 4.6, left).
- Shifting focus to installing "1KwDC" Solar Panel Systems in buildings without existing solar setups, offering significant energy savings through a cost-efficient and feasible strategy.

## 6. Conclusion

Installing '1KwDC' solar panels in buildings without existing systems reduced energy consumption by 28%, proving to be the most cost-effective solution compared to alternatives like insulation upgrades or appliance efficiency enhancements.

Solar panels:
- Reduce reliance on traditional energy sources.
- Are scalable and adaptable to various building types.
- Offer long-term sustainable energy generation.

Other methods, though viable, involve higher costs and extensive modifications.

[Shiny App Link](https://keerthikrishnaaiyappan.shinyapps.io/ShinyApp/)
