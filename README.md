# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 


### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:
```
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# =========================
# Load dataset
# =========================
df = pd.read_csv('/content/amazon_sales_dataset.csv')

df.columns = df.columns.str.strip().str.lower()
df['order_date'] = pd.to_datetime(df['order_date'])

# Combine duplicate dates
df = df.groupby('order_date')['total_revenue'].sum().to_frame()
df = df.sort_index()

# Make data continuous
df = df.resample('D').interpolate()

# =========================
# 1. FIRST FIVE ROWS
# =========================
print("\nFIRST FIVE ROWS:\n")
print(df.head())

# =========================
# 2. PLOTTING THE DATA
# =========================
print("\nPLOTTING THE DATA:\n")

plt.figure(figsize=(8,4))
plt.plot(df['total_revenue'], color='blue')
plt.title('Amazon Revenue Over Time')
plt.xlabel('Date')
plt.ylabel('Revenue')
plt.grid(True)
plt.show()

# =========================
# 3. SEASONAL DECOMPOSITION
# =========================
decomposition = seasonal_decompose(df['total_revenue'], model='additive', period=7)

# =========================
# 3. SEASONAL PLOT
# =========================
print("\nSEASONAL PLOT REPRESENTATION:\n")

plt.figure(figsize=(8,4))
plt.plot(decomposition.seasonal, color='green')
plt.title('Seasonal Component')
plt.grid(True)
plt.show()

# =========================
# 4. TREND PLOT
# =========================
print("\nTREND PLOT REPRESENTATION:\n")

plt.figure(figsize=(8,4))
plt.plot(decomposition.trend, color='orange')
plt.title('Trend Component')
plt.grid(True)
plt.show()

# =========================
# 5. OVERALL REPRESENTATION
# =========================
print("\nOVERALL REPRESENTATION:\n")

decomposition.plot()
plt.show()
```
















### OUTPUT:
FIRST FIVE ROWS:

<img width="287" height="176" alt="image" src="https://github.com/user-attachments/assets/ba99b064-efe8-4418-9457-11a8f7aa66ee" />


PLOTTING THE DATA:

<img width="768" height="445" alt="image" src="https://github.com/user-attachments/assets/1cd9e303-2224-47c2-9089-2c3babe79554" />



SEASONAL PLOT REPRESENTATION :

<img width="731" height="433" alt="image" src="https://github.com/user-attachments/assets/71b2d72a-66b0-4920-b85b-bfac651cb697" />


TREND PLOT REPRESENTATION :
<img width="724" height="423" alt="image" src="https://github.com/user-attachments/assets/39aa0222-2f99-44c1-b67e-f573dfac34fe" />


OVERAL REPRESENTATION:

<img width="700" height="524" alt="image" src="https://github.com/user-attachments/assets/6df3d521-3df8-43d3-8778-60c46ad375f7" />



### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
