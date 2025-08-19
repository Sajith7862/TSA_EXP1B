# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
# NAME: MOHAMED HAMEEM SAJITH J
# REG NO: 212223240090
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load and preprocess the data
data = pd.read_csv('/content/AirPassengers.csv')
data.head()
data['Month'] = pd.to_datetime(data['Month'])
data.set_index('Month', inplace=True)

# Apply transformations
data['passengers_diff'] = data['#Passengers'] - data['#Passengers'].shift(1)
result = seasonal_decompose(data['#Passengers'], model='additive', period=12)
data['passengers_sea_diff'] = result.resid
data['passengers_log'] = np.log(data['#Passengers'])
data['passengers_log_diff'] = data['passengers_log'] - data['passengers_log'].shift(1)
result = seasonal_decompose(data['passengers_log_diff'].dropna(), model='additive', period=12)
data['passengers_log_seasonal_diff'] = result.resid

# Create plots
plt.figure(figsize=(16, 16))

# Original data
plt.subplot(6, 1, 1)
plt.plot(data['#Passengers'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Year')
plt.ylabel('No of passengers')

# Regular differencing
plt.subplot(6, 1, 2)
plt.plot(data['passengers_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced No of passengers')

# Seasonal adjustment
plt.subplot(6, 1, 3)
plt.plot(data['passengers_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally adjusted No of passengers')

# Log transformation
plt.subplot(6, 1, 4)
plt.plot(data['passengers_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(No of passengers)')

# Log transformation and regular differencing
plt.subplot(6, 1, 5)
plt.plot(data['passengers_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('RDiff(Log(No of passengers))')

# Log transformation, regular differencing, and seasonal differencing
plt.subplot(6, 1, 6)
plt.plot(data['passengers_log_seasonal_diff'], label='Log Transformation and regular Diff')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing and Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('SDiff(RDiff(Log(No of passengers)))')

# Display plots
plt.tight_layout()
plt.show()

# Plot all columns
data.plot(kind='line')
```

### OUTPUT:

# ORGINAL DATA:
<img width="1356" height="229" alt="image" src="https://github.com/user-attachments/assets/8b079998-31ac-4e90-a621-1dbca3fec41a" />

# REGULAR DIFFERENCING:

<img width="1371" height="230" alt="image" src="https://github.com/user-attachments/assets/505e7e62-10d4-4c4f-829f-8959ac1403c7" />

# SEASONAL ADJUSTMENT:
<img width="1355" height="253" alt="image" src="https://github.com/user-attachments/assets/07971684-5b95-4bf9-b6c0-2f17351f7631" />


# LOG TRANSFORMATION:
<img width="1368" height="219" alt="image" src="https://github.com/user-attachments/assets/9b403228-fe92-4e14-a2d5-df1d425f57fc" />

# After log transformation and regular differencing:
<img width="1356" height="243" alt="image" src="https://github.com/user-attachments/assets/b268e4dd-190c-42c1-a3fc-d3b1668f3a40" />

#  After log transformation, regular differencing and seasonal differencing:
<img width="1369" height="255" alt="image" src="https://github.com/user-attachments/assets/559c067f-fdbc-4cd0-a902-e023f489b4db" />

# OVERALL VIEW :
<img width="783" height="591" alt="image" src="https://github.com/user-attachments/assets/fa4af810-0614-468f-99e0-982f134417f6" />

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
