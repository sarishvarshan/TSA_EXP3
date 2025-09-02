# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
# Date: 02-09-2025
# Name: Sarish Varshan V
# Reg No: 212223230196
### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

data = pd.read_csv('/content/blood_donor_dataset.csv')

data['created_at'] = pd.to_datetime(data['created_at'])
data = data.set_index('created_at')

daily_counts = data.resample('D').size()

N = len(daily_counts)
lags = range(min(35, N // 2)) 

autocorr_values = []

time_series_data = daily_counts

mean_data = np.mean(time_series_data)
variance_data = np.var(time_series_data)

normalized_data = (time_series_data - mean_data) / np.sqrt(variance_data) if variance_data != 0 else (time_series_data - mean_data)


for lag in lags:
    if lag == 0:
        autocorr_values.append(1)
    else:

        auto_cov = np.sum((time_series_data[:-lag] - mean_data) * (time_series_data[lag:] - mean_data)) / N
 
        autocorr_values.append(auto_cov / variance_data if variance_data != 0 else 0)


plt.figure(figsize=(10, 6))
plt.stem(lags, autocorr_values)
plt.title('Autocorrelation of Daily Entry Counts')
plt.xlabel('Lag (Days)')
plt.ylabel('Autocorrelation')
plt.grid(True)
plt.show()
```
## OUTPUT:
<img width="1170" height="702" alt="image" src="https://github.com/user-attachments/assets/1f82b806-d958-4ec5-8adf-24060903ad18" />

## RESULT:
        Thus we have successfully implemented the auto correlation function in python.
