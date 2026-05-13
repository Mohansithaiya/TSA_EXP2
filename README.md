# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Date: 02/05/2026
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
A - LINEAR TREND ESTIMATION
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

data = pd.read_excel('/content/Hyderabad-AirQ.xlsx')

data['Date'] = pd.to_datetime(data['Date'])

data.set_index('Date', inplace=True)

resampled_data = data['PM2.5'].resample('ME').mean().to_frame()

resampled_data = resampled_data.dropna()

resampled_data.reset_index(inplace=True)

resampled_data.rename(
    columns={'Date':'Month', 'PM2.5':'Air_Quality'},
    inplace=True
)

x = np.arange(len(resampled_data))

y = resampled_data['Air_Quality'].values

linear_coeff = np.polyfit(x, y, 1)

linear_trend = np.polyval(linear_coeff, x)

print("Linear Trend Equation:")

print(f"y = {linear_coeff[0]:.2f}x + {linear_coeff[1]:.2f}")

resampled_data['Linear Trend'] = linear_trend

plt.figure(figsize=(12,6))

plt.plot(
    resampled_data['Month'],
    resampled_data['Air_Quality'],
    color='blue',
    marker='o',
    linewidth=3,
    label='Original Data'
)

plt.plot(
    resampled_data['Month'],
    resampled_data['Linear Trend'],
    color='red',
    linestyle='--',
    marker='s',
    linewidth=2,
    label='Linear Trend'
)

plt.title('Linear Trend Estimation')

plt.xlabel('Month')

plt.ylabel('PM2.5')

plt.legend()

plt.grid(True)

plt.show()
```
B- POLYNOMIAL TREND ESTIMATION
```
poly_coeff = np.polyfit(x, y, 2)

poly_trend = np.polyval(poly_coeff, x)

print("Polynomial Trend Equation:")

print(
    f"y = {poly_coeff[0]:.2f}x² + "
    f"{poly_coeff[1]:.2f}x + "
    f"{poly_coeff[2]:.2f}"
)

resampled_data['Polynomial Trend'] = poly_trend

plt.figure(figsize=(12,6))

plt.plot(
    resampled_data['Month'],
    resampled_data['Air_Quality'],
    color='blue',
    marker='o',
    linewidth=3,
    label='Original Data'
)

plt.plot(
    resampled_data['Month'],
    resampled_data['Polynomial Trend'],
    color='green',
    linestyle=':',
    marker='^',
    linewidth=2,
    label='Polynomial Trend'
)

plt.title('Polynomial Trend Estimation')

plt.xlabel('Month')

plt.ylabel('PM2.5')

plt.legend()

plt.grid(True)

plt.show()
```
### OUTPUT
A - LINEAR TREND ESTIMATION
<img width="1005" height="547" alt="image" src="https://github.com/user-attachments/assets/34d3a8d2-cb61-4552-b7d3-687840727bfd" />

B- POLYNOMIAL TREND ESTIMATION
<img width="1005" height="547" alt="image" src="https://github.com/user-attachments/assets/70d3e71d-8695-4b0e-8008-318e19471213" />

### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
