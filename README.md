Exp 5 : Perform Time Series Analysis and Apply Various Visualization Techniques

AIM:
To perform time series analysis on a dataset, and apply different visualization techniques to understand trends, seasonality, and patterns in the data.

EQUIPMENTS REQUIRED:
Python (Jupyter Notebook or IDE)
Libraries: pandas, matplotlib, seaborn, statsmodels
Dataset URL: Stock Price Data


ALGORITHM:
Load the dataset from a URL.
Convert the date column into a datetime format and set it as the index.
Perform basic analysis like checking for missing values and statistical summary.
Visualize the stock price over time.
Decompose the time series into trend, seasonality, and residual components using statsmodels.
Create rolling statistics (moving average) for smoothing.
Plot the rolling mean along with the original series.


Program:

# Step 1: Import required libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.api as sm

# Step 2: Load dataset from URL
url = "https://raw.githubusercontent.com/selva86/datasets/master/Google_Stock_Price_After_2006.csv"
df = pd.read_csv(url)

# Step 3: Display first few records
print("First few records of the dataset:")
print(df.head())

# Step 4: Convert 'Date' column to datetime and set as index
df['Date'] = pd.to_datetime(df['Date'])
df.set_index('Date', inplace=True)

# Step 5: Check for missing values
print("\nMissing values in the dataset:")
print(df.isnull().sum())

# Step 6: Summary statistics
print("\nSummary statistics of the dataset:")
print(df.describe())

# Step 7: Plot the stock price data over time
plt.figure(figsize=(10, 6))
plt.plot(df.index, df['Close'], label='Stock Price', color='blue')
plt.title("Google Stock Price Over Time")
plt.xlabel("Date")
plt.ylabel("Stock Price")
plt.legend()
plt.grid(True)
plt.show()

# Step 8: Decompose the time series into trend, seasonality, and residuals
decomposition = sm.tsa.seasonal_decompose(df['Close'], model='multiplicative', period=365)
fig = decomposition.plot()
plt.tight_layout()
plt.show()

# Step 9: Rolling Mean and Standard Deviation (Smoothing the data)
rolling_mean = df['Close'].rolling(window=30).mean()
rolling_std = df['Close'].rolling(window=30).std()

# Step 10: Plot rolling mean and original stock price
plt.figure(figsize=(10, 6))
plt.plot(df['Close'], label='Original Stock Price', color='blue')
plt.plot(rolling_mean, label='Rolling Mean (30 days)', color='red')
plt.title("Google Stock Price with Rolling Mean")
plt.xlabel("Date")
plt.ylabel("Stock Price")
plt.legend()
plt.grid(True)
plt.show()


EXPECTED OUTPUT:
Dataset Overview:
Display the first few rows of the dataset.
Show the missing values (if any).
Summary statistics for the stock price (e.g., mean, standard deviation).
Visualization of Stock Prices:
A line plot showing the stock price (Close) over time.
Decomposition of Time Series:
The seasonal decomposition plot with three components:
Trend
Seasonality
Residual
Rolling Mean and Standard Deviation:
A plot showing the original stock price along with a 30-day rolling mean.



RESULT:
The experiment demonstrates how to analyze a time series dataset (stock prices) by decomposing it into trend and seasonal components. Additionally, it shows how to smooth the data using a rolling mean.
