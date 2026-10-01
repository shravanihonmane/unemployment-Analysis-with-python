import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
df = pd.read_csv("Unemployment in India.csv")

# Clean column names
df.columns = df.columns.str.strip()

# Remove extra spaces from text columns
for col in df.select_dtypes(include="object").columns:
    df[col] = df[col].str.strip()

print("First 5 rows:")
print(df.head())

print("\nDataset Information:")
print(df.info())

# Convert unemployment rate to numeric
rate_col = "Estimated Unemployment Rate (%)"
df[rate_col] = pd.to_numeric(df[rate_col], errors="coerce")

# Average unemployment rate
print("\nAverage Unemployment Rate:")
print(df[rate_col].mean())

# Highest unemployment rate
print("\nHighest Unemployment Rate:")
print(df[rate_col].max())

# Monthly trend
df["Date"] = pd.to_datetime(df["Date"], errors="coerce", dayfirst=True)

monthly = df.groupby("Date")[rate_col].mean()

plt.figure(figsize=(10, 5))
plt.plot(monthly.index, monthly.values, marker="o")
plt.title("Unemployment Rate Trend in India")
plt.xlabel("Date")
plt.ylabel("Unemployment Rate (%)")
plt.xticks(rotation=45)
plt.tight_layout()
plt.savefig("unemployment_trend.png", dpi=200)
plt.show()

# State-wise average unemployment
state_avg = (
    df.groupby("Region")[rate_col]
    .mean()
    .sort_values(ascending=False)
    .head(10)
)

plt.figure(figsize=(10, 6))
state_avg.plot(kind="bar")
plt.title("Top 10 Regions by Average Unemployment Rate")
plt.xlabel("Region")
plt.ylabel("Average Unemployment Rate (%)")
plt.xticks(rotation=45)
plt.tight_layout()
plt.savefig("regional_unemployment.png", dpi=200)
plt.show()

print("\nAnalysis completed successfully.")