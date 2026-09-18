Exploratory Data Analysis (EDA) – Shopify Stock Data
1. Project Title
Exploratory Data Analysis on Shopify Stock Data

2. Objective
The objective of this task is to perform Exploratory Data Analysis (EDA) on Shopify stock market data. The dataset contains daily stock information such as Open, High, Low, Close, Adjusted Close and Trading Volume.

The analysis includes data loading, data inspection, data cleaning, feature creation, descriptive statistics, return analysis and data visualization.

3. Technologies Used
Python
Google Colab / Jupyter Notebook
Pandas
Matplotlib
CSV Dataset
4. Dataset
Dataset Name: SHOP.csv

The dataset contains Shopify stock information.

Main Columns
Column	Description
date	Trading date
open	Opening stock price
high	Highest stock price of the day
low	Lowest stock price of the day
close	Closing stock price
adj_close	Adjusted closing price
volume	Number of shares traded
The dataset initially contains 2469 rows and 7 columns.

5. Operations Performed
Operation 1 – Import Libraries
Code
import pandas as pd
import matplotlib.pyplot as plt
Purpose
Pandas is used for data loading and data manipulation. Matplotlib is used for creating graphs and visualizations.

Operation 2 – Load Dataset
Code
df = pd.read_csv("/content/SHOP.csv")
Purpose
The Shopify stock CSV file is loaded into a Pandas DataFrame.

Operation 3 – Display First Five Records
Code
print(df.head())
Output
                        date   open   high    low  close  adj_close     volume
0  2015-05-21 00:00:00-04:00  2.800  2.874  2.411  2.568      2.568  123039000
1  2015-05-22 00:00:00-04:00  2.607  3.110  2.600  2.831      2.831   28412000
2  2015-05-26 00:00:00-04:00  2.980  3.034  2.908  2.965      2.965    8202000
3  2015-05-27 00:00:00-04:00  3.067  3.081  2.700  2.750      2.750    7976000
4  2015-05-28 00:00:00-04:00  2.755  2.774  2.648  2.745      2.745    4000000
Result
The first five rows of the dataset were displayed successfully.

6. Dataset Shape
Code
print(df.shape)
Output
(2469, 7)
Result
The dataset contains:

Rows: 2469
Columns: 7
7. Dataset Information
Code
print(df.info())
Output
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 2469 entries, 0 to 2468
Data columns (total 7 columns):

date        2469 non-null   object
open        2469 non-null   float64
high        2469 non-null   float64
low         2469 non-null   float64
close       2469 non-null   float64
adj_close   2469 non-null   float64
volume      2469 non-null   int64
Result
The dataset contains:

1 date column
5 floating-point price columns
1 integer volume column
8. Missing Value Checking
Code
print(df.isnull().sum())
Output
date         0
open         0
high         0
low          0
close        0
adj_close    0
volume       0
dtype: int64
Result
There are no missing values in the original dataset.

9. Remove Duplicate Records
Code
df = df.drop_duplicates()
Purpose
Duplicate records are removed to improve data quality and avoid repeated observations during analysis.

10. Convert Date Column
Code
df["date"] = pd.to_datetime(
    df["date"],
    format="mixed",
    errors="coerce"
)
Purpose
The date column is converted into a datetime format so that it can be sorted and used as a time-series index.

11. Sort Data by Date
Code
df = df.sort_values("date")
Purpose
The stock records are arranged chronologically.

12. Set Date as Index
Code
df = df.set_index("date")
Purpose
The date column is made the DataFrame index, which is useful for time-series analysis and visualization.

13. Remove Missing Values
Code
df = df.dropna()
Purpose
Any remaining rows containing missing values are removed.

After cleaning, the dataset contains 2469 records with 6 data columns and the date as the index.

14. Feature Engineering
Three new features were created.

14.1 Daily Price Change
Code
df["Daily_Price_'Change"] = df["close"] - df["open"]
This calculates the difference between the closing price and opening price.

14.2 Daily Return Percentage
Code
df["Daily_Return_%"] = ((df["close"] - df["open"]) / df["open"]) * 100
This calculates the daily percentage return.

14.3 Price Range
Code
df["Price_Range"] = df["high"] - df["low"]
This calculates the difference between the highest and lowest price of the day.

15. Display Processed Data
Code
df.head()
Sample Output
Date	Open	High	Low	Close	Daily Price Change	Daily Return %	Price Range
2015-05-21	2.800	2.874	2.411	2.568	-0.232	-8.2857	0.463
2015-05-22	2.607	3.110	2.600	2.831	0.224	8.5923	0.510
2015-05-26	2.980	3.034	2.908	2.965	-0.015	-0.5034	0.126
2015-05-27	3.067	3.081	2.700	2.750	-0.317	-10.3358	0.381
2015-05-28	2.755	2.774	2.648	2.745	-0.010	-0.3630	0.126
16. Descriptive Statistics
Code
print(df.describe())
Important Output
Statistic	Open	High	Low	Close
Count	2469	2469	2469	2469
Mean	48.464	49.505	47.348	48.457
Minimum	1.939	1.985	1.848	1.933
Maximum	171.800	176.292	168.510	169.060
The descriptive statistics also include volume, daily price change, daily return percentage and price range.

17. Mean Daily Return
Code
print("Mean Return:",
      df["Daily_Return_%"].mean())
Output
Mean Return: 0.08640631099421993
Result
The mean daily return is approximately 0.0864%.

18. Return Variance
Code
print("Return Variance:",
      df["Daily_Return_%"].var())
Output
Return Variance: 9.733081984179565
19. Return Standard Deviation
Code
print("Return Standard Deviation:",
      df["Daily_Return_%"].std())
Output
Return Standard Deviation: 3.1197887723657773
The standard deviation measures the variation in daily returns.

20. Trading Volume Trend
Code
plt.figure(figsize=(12,5))
plt.plot(df.index, df["volume"])
plt.title("Shopify Trading Volume Trend")
plt.xlabel("Date")
plt.ylabel("Volume")
plt.xticks(rotation=45)
plt.show()
Output
A line graph showing the Shopify trading volume trend over time.

image
Purpose
This visualization helps examine how trading volume changes across the available dates.

21. Daily Return Distribution
Code
plt.figure(figsize=(12,5))
plt.hist(df["Daily_Return_%"], bins=30)
plt.title("Shopify Daily Return Distribution")
plt.xlabel("Daily Return (%)")
plt.ylabel("Frequency")
plt.show()
Output
A histogram showing the distribution of Shopify's daily returns.

image
Purpose
The histogram helps understand the frequency and spread of daily returns.

22. Price Range Trend
Code
plt.figure(figsize=(12, 5))
plt.plot(df.index, df["Price_Range"])
plt.title("Shopify Stock Price Trend")
plt.xlabel("date")
plt.ylabel("Price_Range")
plt.xticks(rotation=45)
plt.show()
Output
A line graph showing the variation in the daily price range.

image
23. OHLC Price Visualization
Code
import matplotlib.pyplot as plt

plt.figure(figsize=(12,5))
plt.plot(df.index, df["open"], label="Open")
plt.plot(df.index, df["high"], label="High")
plt.plot(df.index, df["low"], label="Low")
plt.plot(df.index, df["open"], label="Close")

plt.title("Shopify OHLC Prices")
plt.xlabel("Date")
plt.ylabel("Price")
plt.legend()
plt.xticks(rotation=45)
plt.show()
Output
A line chart displaying the stock price values over time.

image
Purpose
The visualization compares the Open, High, Low and Close price values.

24. Moving Average
Code
df["MA_20"] = df["close"].rolling(20).mean()

df["MA_50"] = df["close"].rolling(50).mean()
Purpose
Two moving averages are calculated:

20-Day Moving Average
50-Day Moving Average
Moving averages help observe the general movement of the closing price.

25. Closing Price and Moving Averages
Code
plt.figure(figsize=(12,5))

plt.plot(df.index, df["close"], label="Daily Close")
plt.plot(df.index, df["MA_20"], label="20-Day MA")
plt.plot(df.index, df["MA_50"], label="50-Day MA")

plt.title("Shopify Closing Price and Moving Averages")
plt.xlabel("Date")
plt.ylabel("Price")
plt.legend()
plt.xticks(rotation=45)
plt.show()
Output
A line graph comparing:

Daily closing price
20-day moving average
50-day moving average
image
26. KDE of Daily Returns
Code
plt.figure(figsize=(10,5))

df["Daily_Return_%"].plot(kind="kde")

plt.title("KDE of Shopify Daily Returns")
plt.xlabel("Daily Return (%)")

plt.show()
Output
A KDE plot showing the estimated distribution of Shopify's daily returns.

image
27. EDA Summary
The following EDA operations were performed:

Imported Pandas and Matplotlib.
Loaded the Shopify stock CSV dataset.
Displayed the first five records.
Checked the dataset shape.
Checked column information and data types.
Checked missing values.
Removed duplicate records.
Converted the date column to datetime.
Sorted the data by date.
Set the date as the index.
Removed remaining missing values.
Created Daily Price Change.
Created Daily Return Percentage.
Created Price Range.
Generated descriptive statistics.
Calculated mean daily return.
Calculated return variance.
Calculated return standard deviation.
Visualized trading volume.
Visualized daily return distribution.
Visualized price range.
Visualized OHLC prices.
Calculated 20-day and 50-day moving averages.
Visualized closing price with moving averages.
Created a KDE plot for daily returns.
28. Key Results
The dataset contains 2469 records and initially has 7 columns.
No missing values were found in the original dataset.
The date column was processed for time-series analysis.
Three additional analytical features were created.
Mean daily return: 0.0864%
Return variance: 9.7331
Return standard deviation: 3.1198
Multiple graphs were created to understand trading volume, returns, price range and stock-price movement.
29. Conclusion
The EDA provided an overview of Shopify's historical stock data. Data cleaning and preprocessing were performed before calculating additional financial features. Statistical measures were used to understand the distribution and variability of returns, while graphical visualizations helped examine stock prices, trading volume, price ranges and moving averages.

This analysis demonstrates how Python, Pandas and Matplotlib can be used to explore and understand financial time-series data.
