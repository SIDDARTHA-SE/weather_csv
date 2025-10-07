# weather_csv
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Load Data
df = pd.read_csv('weather.csv')
df['date'] = pd.to_datetime(df['date'])

# 2. Data Cleaning
df = df.dropna(subset=['temperature', 'rainfall'])

# 3. EDA
print(df.describe())
plt.figure(figsize=(10,5))
plt.plot(df['date'], df['temperature'])
plt.title('Temperature Over Time')
plt.xlabel('Date')
plt.ylabel('Temp (°C)')
plt.show()

# 4. Monthly Averages
df['month'] = df['date'].dt.month
monthly_avg = df.groupby('month')['rainfall'].mean()
monthly_avg.plot(kind='bar')
plt.title('Average Monthly Rainfall')
plt.show()

# 5. Correlation
sns.heatmap(df.corr(), annot=True)
plt.show()
