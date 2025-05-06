# PROJECT-BASED

# AIM
To perform data preprocessing and exploratory data analysis on the tips dataset using visualization tools in Python.

# CODE

```
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.preprocessing import MinMaxScaler, PowerTransformer

# Load the dataset
df = sns.load_dataset("tips")

# Check for null values
print("Null Values:\n", df.isnull().sum())

# Detect outliers using IQR method for 'total_bill' and 'tip'
Q1 = df[['total_bill', 'tip']].quantile(0.25)
Q3 = df[['total_bill', 'tip']].quantile(0.75)
IQR = Q3 - Q1
outliers = ((df[['total_bill', 'tip']] < (Q1 - 1.5 * IQR)) | (df[['total_bill', 'tip']] > (Q3 + 1.5 * IQR)))
print("\nOutliers Detected:\n", outliers.any())

# Remove outliers
df = df[~((df[['total_bill', 'tip']] < (Q1 - 1.5 * IQR)) | (df[['total_bill', 'tip']] > (Q3 + 1.5 * IQR))).any(axis=1)]

# Feature transformation (Log transform total_bill)
df['log_total_bill'] = PowerTransformer().fit_transform(df[['total_bill']])

# Feature scaling (MinMax scaling of tip)
scaler = MinMaxScaler()
df['scaled_tip'] = scaler.fit_transform(df[['tip']])

# 1. Bar plot: Day vs Total bill
plt.figure(figsize=(6,4))
sns.barplot(x='day', y='total_bill', data=df, estimator=sum)
plt.title('Total Bill by Day')
plt.show()

# 2. Box plot: Smoker vs Tip
plt.figure(figsize=(6,4))
sns.boxplot(x='smoker', y='tip', data=df)
plt.title('Tip by Smoker/Non-Smoker')
plt.show()

# 3. Scatter plot: Tip% vs Size
df['tip_percent'] = (df['tip'] / df['total_bill']) * 100
plt.figure(figsize=(6,4))
sns.scatterplot(x='size', y='tip_percent', data=df)
plt.title('Tip % vs Party Size')
plt.show()

# 4. Box plot: Gender vs Tip
plt.figure(figsize=(6,4))
sns.boxplot(x='sex', y='tip', data=df)
plt.title('Tip by Gender')
plt.show()

# 5. Scatter plot: Total Bill vs Day
plt.figure(figsize=(6,4))
sns.stripplot(x='day', y='total_bill', data=df, jitter=True)
plt.title('Total Bill vs Day')
plt.show()

# 6. Hist plot: Total bill by time
plt.figure(figsize=(6,4))
sns.histplot(data=df, x='total_bill', hue='time', kde=True)
plt.title('Total Bill Distribution by Time')
plt.show()

# 7. Line plot: Avg total bill by size
plt.figure(figsize=(6,4))
avg_bill = df.groupby('size')['total_bill'].mean().reset_index()
sns.lineplot(x='size', y='total_bill', data=avg_bill, marker='o')
plt.title('Average Total Bill by Party Size')
plt.show()

# 8. Box plot: Tip by day
plt.figure(figsize=(6,4))
sns.boxplot(x='day', y='tip', data=df)
plt.title('Tip Distribution by Day')
plt.show()

# 9. Violin plot: Tip by time
plt.figure(figsize=(6,4))
sns.violinplot(x='time', y='tip', data=df)
plt.title('Tip by Lunch vs Dinner')
plt.show()

# 10. Scatter plot: Tip vs Total bill
plt.figure(figsize=(6,4))
sns.scatterplot(x='total_bill', y='tip', data=df)
plt.title('Total Bill vs Tip')
plt.show()
```

# EXECUTION & OUTPUT

![image](https://github.com/user-attachments/assets/fef7df47-eab8-4ac6-974f-16299643a632)

## 1. Bar plot: Day vs Total bill

![image](https://github.com/user-attachments/assets/863b8c97-f33e-42f4-9ce3-584691415f90)

## 2. Box plot: Smoker vs Tip

![image](https://github.com/user-attachments/assets/3851f6eb-490a-4fbc-8086-f3381d9c9603)

## 3. Scatter plot: Tip% vs Size

![image](https://github.com/user-attachments/assets/aa1c0181-1b26-438b-8e98-9106f27b3d64)

## 4. Box plot: Gender vs Tip

![image](https://github.com/user-attachments/assets/c9882325-9eba-4c04-95e1-ca3f8445bdc1)

## 5. Scatter plot: Total Bill vs Day

![image](https://github.com/user-attachments/assets/a8cf2f9e-b3aa-451d-9caf-9957dd0556ba)

## 6. Hist plot: Total bill by time

![image](https://github.com/user-attachments/assets/34594a4d-a39a-40d0-8e6d-bb2288836a22)

## 7. Line plot: Avg total bill by size

![image](https://github.com/user-attachments/assets/39d5ed4c-ec61-4993-85a4-97daedb92fa8)

## 8. Box plot: Tip by day

![image](https://github.com/user-attachments/assets/23080857-2906-4d29-8d16-51d19a7377ec)

## 9. Violin plot: Tip by time

![image](https://github.com/user-attachments/assets/4d7c127a-2f53-4c96-b08d-9fad2b1d7041)

## 10. Scatter plot: Tip vs Total bill

![image](https://github.com/user-attachments/assets/13a1267b-b975-43fa-bb93-10b4f67d01c0)

# RESULT
The analysis of the tips dataset was completed successfully. Insights on tip behavior and patterns based on various attributes were derived using visualization techniques.
