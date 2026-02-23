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
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Step 1: Load the dataset
data = pd.read_csv("/kaggle/input/time-series/daily-minimum-temperatures-in-me.csv", 
                   on_bad_lines='skip')

data.columns = ["Date", "Temp"]
data["Date"] = pd.to_datetime(data["Date"])
data.set_index("Date", inplace=True)

# ----------------------------------------
# FIX INVALID TEMPERATURE VALUES
# ----------------------------------------

# Remove special characters like ? and convert to numeric
data["Temp"] = data["Temp"].astype(str).str.replace("?", "", regex=False)

# Convert to numeric (coerce errors → NaN)
data["Temp"] = pd.to_numeric(data["Temp"], errors='coerce')

# Drop rows with NaN
data.dropna(inplace=True)

# ----------------------------------------
# Step 2: Seasonal Decomposition
# ----------------------------------------
decomposition = seasonal_decompose(data["Temp"], model="additive", period=365)

# Step 3: Plot the decomposition
plt.figure(figsize=(10, 12))

# Original Data
plt.subplot(411)
plt.plot(data["Temp"], label='Daily Temperature')
plt.legend(loc='upper left')
plt.title("Original Temperature Data")

# Trend
plt.subplot(412)
plt.plot(decomposition.trend, label='Trend', color='orange')
plt.legend(loc='upper left')
plt.title("Trend Plot")

# Seasonality
plt.subplot(413)
plt.plot(decomposition.seasonal, label='Seasonal', color='green')
plt.legend(loc='upper left')
plt.title("Seasonality Plot")

# Residuals
plt.subplot(414)
plt.plot(decomposition.resid, label='Residual', color='red')
plt.legend(loc='upper left')
plt.title("Residual Plot")

plt.tight_layout()
plt.show()

```

### OUTPUT:
<img width="840" height="293" alt="image" src="https://github.com/user-attachments/assets/aa313f55-384e-45af-8393-4169dda80b35" />

<img width="631" height="185" alt="image" src="https://github.com/user-attachments/assets/9242253d-0cba-468d-b360-a471cdbcea2e" />

<img width="572" height="170" alt="image" src="https://github.com/user-attachments/assets/b48d81df-20aa-4ee7-adb3-c5d9d501e644" />

<img width="706" height="134" alt="image" src="https://github.com/user-attachments/assets/0228c4a7-b600-4f33-a9b0-eb96ea7e37a0" />

### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
