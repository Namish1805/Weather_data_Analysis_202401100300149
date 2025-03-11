# Weather Data Analysis  

## Introduction  
This project focuses on analyzing weather data using Python. It involves data preprocessing, visualization, anomaly detection, and forecasting trends using a moving average.  

## Features  
- *Data Cleaning & Preprocessing*: Handles missing values by filling them with the mean.  
- *Weather Trends Visualization*: Plots temperature, humidity, and rainfall over time.  
- *Correlation Analysis*: Uses a heatmap to show relationships between weather variables.  
- *Anomaly Detection*: Identifies unusual weather conditions using Z-score analysis.  
- *Moving Average Forecasting*: Computes a 7-day moving average for temperature trends.  

## Methodology  

1. *Data Collection & Preprocessing*  
   - The weather dataset is loaded from an Excel file (weather_data.csv.xlsx).  
   - The Date column is converted to a datetime format and set as the index.  
   - Missing values are handled by filling them with the mean of the respective column.  

2. *Data Visualization*  
   - A *line plot* is used to display trends in temperature, rainfall, and humidity over time.  
   - A *correlation heatmap* is generated to analyze relationships between weather parameters.  

3. *Anomaly Detection*  
   - The *Z-score method* is applied to detect anomalies in the data.  
   - Any data points with Z-scores greater than 2 or less than -2 are flagged as anomalies.  

4. *Forecasting (Moving Average)*  
   - A *7-day moving average* is calculated to smooth out temperature fluctuations.  
   - The temperature trend is visualized using a moving average line.  

## Code Description  

The Python script follows these steps:  

1. *Import Required Libraries*  
   python
   import pandas as pd
   import matplotlib.pyplot as plt
   import seaborn as sns
   import numpy as np
   

2. *Load & Preprocess the Data*  
   python
   file_path = "weather_data.csv.xlsx"
   df = pd.read_excel(file_path)
   df["Date"] = pd.to_datetime(df["Date"])
   df.set_index("Date", inplace=True)
   df.fillna(df.mean(), inplace=True)
   

3. *Plot Weather Trends*  
   python
   plt.figure(figsize=(12, 6))
   plt.plot(df.index, df["Temperature"], label="Temperature (Â°C)", color="red", marker="o", linestyle="-")
   plt.plot(df.index, df["Rainfall"], label="Rainfall (mm)", color="blue", marker="s", linestyle="dashed")
   plt.plot(df.index, df["Humidity"], label="Humidity (%)", color="green", marker="^", linestyle="dotted")
   plt.title("Weather Trends Over Time")
   plt.xlabel("Date")
   plt.ylabel("Values")
   plt.legend()
   plt.grid(True, linestyle="--", alpha=0.6)
   plt.xticks(rotation=45)
   plt.show()
   

4. *Correlation Heatmap*  
   python
   plt.figure(figsize=(6, 4))
   sns.heatmap(df.corr(), annot=True, cmap="coolwarm", fmt=".2f", linewidths=0.5, linecolor="black")
   plt.title("Correlation Between Weather Variables")
   plt.show()
   

5. *Anomaly Detection Using Z-score*  
   python
   df_mean, df_std = df.mean(), df.std()
   z_scores = (df - df_mean) / df_std
   anomalies = df[(z_scores.abs() > 2).any(axis=1)]
   

6. *Moving Average Forecasting*  
   python
   df["Temperature_MA"] = df["Temperature"].rolling(window=7, min_periods=1).mean()
   plt.figure(figsize=(12, 6))
   plt.plot(df.index, df["Temperature"], label="Daily Temperature", alpha=0.5, color="red")
   plt.plot(df.index, df["Temperature_MA"], label="7-Day Moving Average", color="black", linewidth=2)
   plt.title("Temperature Trend with Moving Average")
   plt.xlabel("Date")
   plt.ylabel("Temperature (Â°C)")
   plt.legend()
   plt.grid(True, linestyle="--", alpha=0.6)
   plt.xticks(rotation=45)
   plt.show()
   

## Technologies Used  
- *Python* for data processing and analysis  
- *Pandas* for handling datasets  
- *Matplotlib & Seaborn* for visualization  
- *NumPy* for numerical computations  


