# Walmart Sales Forecasting

## Table of Contents
[Project Overview](#project-overview)

[Data Sources](#data-sources)

[Data Description](#data-description)

[Tools](#tools)

[EDA Steps](#eda-steps)

[Data Preprocessing Steps and Inspiration](#data-preprocessing-steps-and-inspiration)

[Forecasting of Weekly Sales](#forecasting-of-weekly-sales)

[Assumptions](#assumptions)

[Model Evaluation Metrics](#model-evaluation-metrics)

[Results](#results)

[Recommendations](#recommendations)

[Limitations](#limitations)

[Future Possibilities of the Project](#future-possibilities-of-the-project)

[References](#references)

### Project Overview

The objective of this project is to analyze Walmart sales data to extract meaningful insights and develop predictive models to forecast weekly sales for each store. This analysis aims to help Walmart improve inventory management, strategic decision-making, and overall operational efficiency.

### Data Sources

Walmart Sales Data: The primary dataset used for this analysis is the Walmart.csv file, containing detailed information about weekly sales across multiple Walmart stores.

Walmart Dataset(https://github.com/tgchacko/Walmart-Sales-Forecasting/blob/main/Walmart.csv)

### Data Description

The dataset, named "Walmart.csv", comprises 6,435 rows and 8 columns, each offering valuable insights into the weekly sales dynamics at Walmart across 45 stores. The dataset Walmart.csv contains various columns including:

1) Store: Store number (categorical variable ranging from 1 to 45)
2) Date: The week of sales (temporal dimension spanning from February 5, 2010, to October 26, 2012)
3) Weekly_Sales: Sales figure for the given store in a particular week
4) Holiday_Flag: A binary indicator (0 or 1) discerning whether a given week includes a holiday
5) Temperature: The temperature on the day of the sale
6) Fuel_Price: The regional fuel cost
7) CPI: Consumer Price Index, indicating the average change in prices paid by consumers
8) Unemployment: The unemployment rate in the region

### Tools

- Python: Data Cleaning and Analysis

    [Download Python](https://www.python.org/downloads/)

- Jupyter Notebook: For interactive data analysis and visualization

    [Install Jupyter](https://jupyter.org/install)
 
**Libraries**

Below are the links for details and commands (if required) to install the necessary Python packages:

Below are the links for details and commands (if required) to install the necessary Python packages:
- **pandas**: Go to [Pandas Installation](https://pypi.org/project/pandas/) or use command: `pip install pandas`
- **numpy**: Go to [NumPy Installation](https://pypi.org/project/numpy/) or use command: `pip install numpy`
- **matplotlib**: Go to [Matplotlib Installation](https://pypi.org/project/matplotlib/) or use command: `pip install matplotlib`
- **seaborn**: Go to [Seaborn Installation](https://pypi.org/project/seaborn/) or use command: `pip install seaborn`
- **scikit-learn**: Go to [Scikit-Learn Installation](https://pypi.org/project/scikit-learn/) or use command: `pip install scikit-learn`
- **statsmodels**: Go to [Statsmodels Installation](https://pypi.org/project/statsmodels/) or use command: `pip install statsmodels`
- **pmdarima**: Go to [Pmdarima Installation](https://pypi.org/project/pmdarima/) or use command: `pip install pmdarima`
- **fbprophet**: Go to [Prophet Installation](https://pypi.org/project/fbprophet/) or use command: `pip install fbprophet`
- **tbats**: Go to [TBATS Installation](https://pypi.org/project/tbats/) or use command: `pip install tbats`

### EDA Steps

EDA involved exploring the Walmart sales data to answer key questions, such as:

1) What is the overall trend of weekly sales?
2) How do these trends vary by store, region, and other factors?
3) What is the impact of holidays on weekly sales?
4) How do external factors like temperature, fuel price, CPI, and unemployment affect sales?

### Data Preprocessing Steps and Inspiration
1. #### Data Cleaning:
Handling Missing Values: There are no missing values found in the dataset.
Removing Duplicates: There are no duplicate values found in the dataset.
Addressing Outliers: Outliers are not being addressed since we are considering the actual weekly sales for time series forecasting.

2. ##### Data Transformation:
    Converting Data Types: The data type for the column ‘Date’ is changed to ‘datetime’ from ‘object’. From this date, we have created new columns by obtaining the year, quarter, month, week, day of week, and day of month.

3. #### Exploratory Data Analysis (EDA):

**Data Gaps**: 
Before doing the EDA, we observed that there is a gap in the data for January 2010 and for November, December 2012. The absence of data for these three months can impact our ability to perform accurate yearly, quarterly, and monthly comparisons. The distribution of data is thus affected. It is essential to consider this data gap while conducting analyses that involve these specific time periods.

## Distribution of Data:
        Figure 6: Distribution of data for Walmart across years
        Figure 7: Distribution of data for Walmart across quarters
        Figure 8: Distribution of data across Holidays / Non-Holidays
        Figure 9: Sales distribution over the years, months, weekday, quarterly, working days / holidays

    Store-wise Analysis:
        Figure 10: Store wise Total Sales: Store No. 20 has the highest sales, whereas store No. 33 has the lowest sales. The sales difference between these two stores is shown.
        Figure 11: Code for Top Performing Stores and Lowest Performing Store

    Yearly Analysis:
        Figure 12: Year wise Total Sales

    Monthly Analysis:
        Figure 13: Month wise Total Sales (without adjustment): As there is a gap in the data for January 2010 and for November, December 2012, we would average it out to show for these months which month has the highest sales. After doing the necessary adjustment, we can see that December is the best performing month and February is the worst performing month.
        Figure 14: Code for Monthly Sales (without adjustment)

    Holiday / Working Day Analysis:
        Figure 15: Holiday / Working Day Total Sales (without adjustment): If we make the adjustment by dividing the sales with the actual number of working days and holidays, we can see the daily sales on a holiday is higher.
        Figure 16: Code for Daily Holiday / Working Day Sales

    Impact of Unemployment on Weekly Sales:
        Figure 17: Impact of Unemployment on Sales: The data indicates a noticeable decline in spending coinciding with the initiation of unemployment. Typically, an elevated unemployment index corresponds to a reduction in sales. However, in our dataset, the correlation between the unemployment rate index and weekly sales is relatively low, measuring at -0.106.

    Impact of Temperature on Weekly Sales:
        Figure 18: Impact of Temperature on Sales: The observed correlation of -0.063 between temperature and sales in Walmart suggests a weak negative relationship. Several factors could contribute to this low correlation:
            Seasonal Variations
            Diverse Product Range
            Regional Variations
            Consumer Behavior
            Multifactorial Influence

    Impact of CPI on Weekly Sales:
        Figure 19: Impact of CPI on Sales: The observed low correlation of -0.072 between the Consumer Price Index (CPI) and sales indicates a weak relationship.

    Seasonal Trend of Weekly Sales:
        Figure 20: Seasonal Trend in Weekly Sales: Sales are the highest in December, which can be attributed to several factors:
            Holiday Shopping Season
            Special Promotions and Discounts
            Winter Weather and Seasonal Products
            Year-End Clearance Sales
            Increased Consumer Spending
            Marketing and Advertising Campaigns
            Extended Store Hours
        Figure 21: Trend Component, Seasonal Component, Residual Component of Weekly Sales



### Forecasting of Weekly Sales
### Time Series Forecasting Models

1) **ARIMA (AutoRegressive Integrated Moving Average)**
   - Captures linear trends and seasonality.
   - Suitable for stationary data.
2) **SARIMAX (Seasonal AutoRegressive Integrated Moving Average with eXogenous factors)**
   - Extends ARIMA by incorporating external factors.
   - Suitable for data influenced by external variables like holidays.
3) **AutoARIMA**
   - Automates the selection of the optimal ARIMA model.
   - User-friendly and efficient.
4) **Prophet**
   - Developed by Facebook for handling seasonality, holidays, and special events.
   - Flexible and easy to use.
5) **TBATS (Trigonometric Seasonal Decomposition of Time Series)**
   - Handles multiple seasonalities and complex patterns.
   - Robust in capturing diverse seasonal patterns.
  
### Assumptions

1. **Stationarity Assumption**

    **Definition**: The statistical properties of the time series data, such as mean and variance, do not change over time.
    **Rationale**: Many time series forecasting models, including ARIMA, perform better on stationary data. Ensuring or achieving stationarity enhances model effectiveness.

2. **Linearity Assumption**

    **Definition**: The relationships between variables, including past and future values in the time series, can be adequately represented using linear models.
    **Rationale**: Models like ARIMA and SARIMAX are designed based on linear relationships. Assuming linearity simplifies the modeling process.

3. **Independence Assumption**

    **Definition**: Each observation in the time series is assumed to be independent of others.
    **Rationale**: Time series models often assume independence to prevent past observations from unduly influencing future ones. Violating this assumption can lead to biased model performance.

4. **Identifiability Assumption**

    **Definition**: The parameters of the chosen forecasting model can be uniquely determined from the available data.
    **Rationale**: Ensuring that the parameters are identifiable is crucial for accurate estimation in models like ARIMA and SARIMAX. This supports the reliability of the model's parameter estimates.

### Model Evaluation Metrics

1) RMSE (Root Mean Squared Error): Measures the average magnitude of the errors between predicted and observed values.
2) MAE (Mean Absolute Error): Calculates the average absolute differences between predicted and observed values.
3) MAPE (Mean Absolute Percentage Error): Expresses the average percentage difference between predicted and observed values.

### Results 

**Considering Store 24**
- The TBATS model achieved the best performance metrics (lowest MAPE, RMSE, and MAE) for Store No. 24.
- The analysis highlighted significant trends and seasonal patterns in weekly sales.
- The impact of external factors like unemployment, temperature, and CPI on sales was explored.

### Recommendations

- Implement targeted interventions during peak sales periods and holidays to maximize revenue.
- Continue monitoring external factors to understand their potential impact on sales.
- Utilize the forecasting model to plan inventory management and resource allocation more effectively.

### Limitations

- Data Quality: Some data points may be inaccurate due to underreporting or delays in reporting.
- Model Limitations: The models used may not capture all complexities of sales patterns and may need continuous updating.
- External Factors: Other factors not included in the analysis, such as social behavior and political decisions, can significantly impact sales.

### Future Possibilities of the Project
1. **Advanced Predictive Modeling**

Investigate advanced forecasting models such as:
a) NBEATS (Neural Basis Expansion Analysis for Time Series)
b) NHITS (Neural Hierarchical Time Series)
c) PatchTST (Patch-level Temporal Super-Resolution Network for Time Series)
d) VARMAX (Vector Autoregressive Moving-Average with exogenous variables)
e) VAR (Vector Autoregression)
f) KATS (Kit for Automated Time Series analysis)

These models offer potential for enhanced accuracy in sales forecasting.

2. **Store-Specific Analysis**

Conduct comprehensive analyses for each of the 45 Walmart stores to uncover unique patterns and optimize forecasting models tailored to individual store characteristics. This approach can help identify specific trends and factors influencing sales at each location.

3. **External Factors Integration**
Incorporate Additional Factors: Consider integrating additional external factors into the forecasting models, such as:
1) Economic Indicators: GDP, inflation rates, etc.
2) Social Events: Festivals, public holidays, etc.
3) Regional Factors: Local economic conditions, demographic changes, etc.

Incorporating these factors can provide a more comprehensive and accurate forecasting approach, capturing the broader context influencing sales.

### References

1) [Hyndman, R. J., & Athanasopoulos, G. (2018). Forecasting: principles and practice. OTexts. Forecasting: principles and practice](https://otexts.com/fpp2/)
2) [Time Series forecasting in Python: Time Series Forecasting in Python](https://www.methsoft.ac.cn/scipaper_files/document_files/Manning.Time.Series.Forecasting.in.Python.pdf)
3) [Time Series Forecasting TBATS: TBATS Time Series Forecasting](https://medium.com/analytics-vidhya/time-series-forecasting-using-tbats-model-ce8c429442a9)
