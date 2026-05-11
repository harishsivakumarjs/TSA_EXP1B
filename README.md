# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 11/05/26

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load dataset
data = pd.read_csv(r"C:/Users/admin/Downloads/index_1.csv")

# Clean column names
data.columns = data.columns.str.strip()

# Convert date
data['date'] = pd.to_datetime(data['date'])

# Set index
data.set_index('date', inplace=True)

ts = data['money'].resample('M').sum().dropna()

ts_diff = ts - ts.shift(1)
result = seasonal_decompose(ts, model='additive', period=3)
ts_sea_diff = result.resid

ts_log = np.log(ts.replace(0, np.nan)).dropna()
ts_log_diff = ts_log - ts_log.shift(1)

result = seasonal_decompose(ts_log_diff.dropna(), model='additive', period=3)
ts_log_sea_diff = result.resid

# Plot 6 graphs
plt.figure(figsize=(12,10))

# 1 Original
plt.subplot(6,1,1)
plt.plot(ts)
plt.title('Original Coffee Sales')
plt.xlabel('Date')
plt.ylabel('Revenue')

# 2 Differencing
plt.subplot(6,1,2)
plt.plot(ts_diff)
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Differenced Revenue')

# 3 Seasonal Adjustment
plt.subplot(6,1,3)
plt.plot(ts_sea_diff)
plt.title('Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('Seasonally Adjusted')

# 4 Log
plt.subplot(6,1,4)
plt.plot(ts_log)
plt.title('Log Transformation')
plt.xlabel('Date')
plt.ylabel('Log(Revenue)')

# 5 Log + Diff
plt.subplot(6,1,5)
plt.plot(ts_log_diff)
plt.title('Log + Differencing')
plt.xlabel('Date')
plt.ylabel('RDiff(Log)')

# 6 Final
plt.subplot(6,1,6)
plt.plot(ts_log_sea_diff)
plt.title('Log + Diff + Seasonal')
plt.xlabel('Date')
plt.ylabel('Final Processed')

plt.tight_layout()
plt.show()
```

### OUTPUT:

<img width="1003" height="140" alt="image" src="https://github.com/user-attachments/assets/3836666b-7cd4-4f61-980a-7874f841c8e4" />

REGULAR DIFFERENCING:

<img width="989" height="138" alt="image" src="https://github.com/user-attachments/assets/1fd1188a-fedb-44a0-be7a-8052ea7931eb" />


SEASONAL ADJUSTMENT:

<img width="1004" height="139" alt="image" src="https://github.com/user-attachments/assets/2784a2c7-91f5-488a-86e0-fc69ca772731" />


LOG TRANSFORMATION:

<img width="1011" height="408" alt="image" src="https://github.com/user-attachments/assets/0a4f941b-7741-4630-8a0e-44bbc5167992" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
