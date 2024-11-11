## DEVELOPED BY: M JAYACHANDRAN
## REGISTER NO: 212222240038
## DATE:

# Ex.No: 08     MOVING AVERAGE MODEL AND EXPONENTIAL SMOOTHING
 
## AIM:
To implement Moving Average Model and Exponential smoothing Using Python.
## ALGORITHM:
1. Import necessary libraries
2. Read the House Sales time series data from a CSV file,Display the shape and the first 20 rows of
the dataset
3. Set the figure size for plots
4. Suppress warnings
5. Plot the first 50 values of the 'Value' column
6. Perform rolling average transformation with a window size of 5
7. Display the first 10 values of the rolling mean
8. Perform rolling average transformation with a window size of 10
9. Create a new figure for plotting,Plot the original data and fitted value
10. Show the plot
11. Also perform exponential smoothing and plot the graph
## PROGRAM:
```python
# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing

# Suppress warnings
warnings.filterwarnings('ignore')

# Read the dataset from the uploaded CSV file
file_path = 'future_gold_price.csv'  # Path to the uploaded dataset
data = pd.read_csv(file_path)

# Display the shape and the first few rows of the dataset
print("Shape of the dataset:", data.shape)
print("First 20 rows of the dataset:")
print(data.head(20))

# Ensure the 'Date' column is in datetime format and set it as index
data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)

# Convert the 'Close' column to numeric, removing commas if necessary
data['Close'] = data['Close'].replace(',', '', regex=True).astype(float)

# Plot Original Close Price Data
plt.figure(figsize=(12, 6))
plt.plot(data['Close'], label='Original Close Price', color='blue')
plt.title('Original Close Price Data')
plt.xlabel('Date')
plt.ylabel('Close Price')
plt.legend()
plt.grid()
plt.show()

# Moving Average
# Perform rolling average transformation with a window size of 3 (adjust as needed)
rolling_mean_3 = data['Close'].rolling(window=3).mean()

# Plot Moving Average
plt.figure(figsize=(12, 6))
plt.plot(data['Close'], label='Original Close Price', color='blue')
plt.plot(rolling_mean_3, label='Moving Average (window=3)', color='orange')
plt.title('Moving Average of Close Price')
plt.xlabel('Date')
plt.ylabel('Close Price')
plt.legend()
plt.grid()
plt.show()

# Exponential Smoothing
# Configure the Exponential Smoothing model with additive trend
model = ExponentialSmoothing(data['Close'], trend='add', seasonal=None)
model_fit = model.fit()

# Make predictions for the next 5 periods (adjust as needed)
future_steps = 5
predictions = model_fit.predict(start=len(data), end=len(data) + future_steps - 1)

# Create a future index for the predicted dates
future_dates = pd.date_range(start=data.index[-1] + pd.Timedelta(days=1), periods=future_steps)

# Plot the original data and Exponential Smoothing predictions
plt.figure(figsize=(12, 6))
plt.plot(data['Close'], label='Original Close Price', color='blue')
plt.plot(future_dates, predictions, label='Exponential Smoothing Forecast', color='orange')
plt.title('Exponential Smoothing Predictions for Close Price')
plt.xlabel('Date')
plt.ylabel('Close Price')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()

# Display predictions
print("Future Predictions for Close Price:")
print(predictions)

```

## OUTPUT:
### GIVEN DATA
![Screenshot 2024-11-11 190805](https://github.com/user-attachments/assets/91dd1e13-9163-4a38-ab00-d34b3e1f64e8)


### Moving Average
![Screenshot 2024-11-11 190853](https://github.com/user-attachments/assets/02dedeec-fb27-4ec0-acc4-da71ed817e57)


### Plot Transform Dataset
![Screenshot 2024-11-11 190835](https://github.com/user-attachments/assets/770572c4-7eab-4f3e-9fcc-636f229cf649)


### Exponential Smoothing
![Screenshot 2024-11-11 190909](https://github.com/user-attachments/assets/0f76309f-7fe7-4ec7-a580-d195f3d5492a)



## RESULT:
Thus, the program to implement the Moving Average Model and Exponential smoothing using python is executed successfully.
