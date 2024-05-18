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

[Walmart Dataset](https://github.com/tgchacko/Walmart-Sales-Forecasting/blob/main/Walmart.csv)

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

![Picture1](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/04943f90-1790-4d84-8fde-34bf35d8aa6c)

![Picture2](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/6b067d21-749e-4390-bdd9-cb8bea280124)

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

**Distibution of Data**:

1) **Across Years**

![Picture3](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/38b2ede2-e723-49bb-923a-52411c0db00a)

2) **Across Quarters**
 
![Picture4](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/0d9d0173-b8aa-497a-9beb-eb4c2cf252a1)

3) **Across Holidays/Non Holidays)**
 
![Picture5](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/0a087e49-707f-4055-9c97-654f4e4ab664)

4) **Distribution of Data - Pie Charts**

![Picture6](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/ccbe3b93-0f19-4cb6-ac88-88d02fe71c60)

![Picture7](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/364be7fd-36ee-4231-bb16-32f34dc87ffd)

**Top 5 Performing Stores**

![Picture8](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/ac671636-af2b-4ac9-ae25-de266d197da1)

![Picture9](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/2a727023-a0ee-4402-a52e-65ecf5c93544)

**Worst 5 Performing Stores**

![Picture10](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/722c34fd-12bc-4ab6-bfd7-d300ef33f490)

Store No. 20 has the highest sales, whereas store No. 33 has the lowest sales.


**Total Yearly Sales**

![Picture11](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/5e33fb00-e5b7-40e5-b7ca-1e8acc5eefa1)

**Total Monthly Sales**

![Picture12](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/742d6848-af48-4a24-94cd-a573a48371b7)

As there is a gap in the data for January 2010 and for November, December 2012, we would average it out to show for these months which month has the highest sales. After doing the necessary adjustment, we can see that December is the best performing month and February is the worst performing month.

**Top 5 months with Highest and Lowest Sales**

![Picture13](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/2b5e61ee-646f-4d01-8f14-dc01e6237211)

**Total Holiday/Non-Holiday Sales**

![Picture14](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/05beec3b-9edf-4165-ac29-95569e4ed83f)

If we make the adjustment by dividing the sales with the actual number of working days and holidays, we can see the daily sales on a holiday is higher.

**Average Daily Sales on a Holiday / a Non Holiday**

![Picture15](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/807ceb7c-a301-4f88-9187-05e16e4b0a57)

**Impact of Unemployment on Weekly Sales**

The data indicates a noticeable decline in spending coinciding with the initiation of unemployment. Typically, an elevated unemployment index corresponds to a reduction in sales. However, in our dataset, the correlation between the unemployment rate index and weekly sales is relatively low, measuring at -0.106.

![Picture16](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/5d2d4b17-e19e-4fbd-b07c-e85299c303c0)

**Impact of Temperature on Weekly Sales**

![Picture17](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/5b20f8cf-ad14-4ff7-b86a-bba717452891)

The observed correlation of -0.063 between temperature and sales in Walmart suggests a weak negative relationship. Several factors could contribute to this low correlation:
1) Seasonal Variations
2) Diverse Product Range
3) Regional Variations
4) Consumer Behavior
5) Multifactorial Influence

**Impact of CPI on Weekly Sales**

The observed low correlation of -0.072 between the Consumer Price Index (CPI) and sales indicates a weak relationship.

![Picture18](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/7eeeecd1-3515-4346-9ed9-901e0d0e5dc8)

**Seasonal Trend of Weekly Sales**

![Picture19](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/3d908d41-5656-43d1-a07d-c7fe157ac7f4)

Seasonal Trend in Weekly Sales: Sales are the highest in December, which can be attributed to several factors:
1) Holiday Shopping Season
2) Special Promotions and Discounts
3) Winter Weather and Seasonal Products
4) Year-End Clearance Sales
5) Increased Consumer Spending
6) Marketing and Advertising Campaigns
7) Extended Store Hours

**Trend Component, Seasonal Component, Residual Component of Weekly Sales**

![Picture20](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/95060897-bb11-4ec8-a927-25eb15326926)

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

  ![Picture21](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/6a2b9f02-bfeb-4df0-8674-ff3a4ad8df12)

- The analysis highlighted significant trends and seasonal patterns in weekly sales.
- The impact of external factors like unemployment, temperature, and CPI on sales was explored.
  
![Picture22](https://github.com/tgchacko/Walmart-Sales-Forecasting/assets/169921893/8578bd40-b2a2-4357-bd57-ca6f6fe89b61)

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
