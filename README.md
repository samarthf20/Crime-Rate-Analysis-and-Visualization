import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import random

crime_types = [
    'Theft',
    'Murder',
    'Assault',
    'Robbery',
    'Cyber Crime',
    'Kidnapping',
    'Fraud',
    'Burglary',
    'Drug Trafficking',
    'Domestic Violence'
]

areas = [
    'Bangalore',
    'Mysore',
    'Delhi',
    'Mumbai',
    'Chennai',
    'Hyderabad',
    'Pune',
    'Kolkata',
    'Ahmedabad',
    'Jaipur'
]

years = [2019, 2020, 2021, 2022, 2023, 2024]

data = []

for i in range(500):

    crime = random.choice(crime_types)
    area = random.choice(areas)
    year = random.choice(years)

    data.append([crime, year, area])

df = pd.DataFrame(
    data,
    columns=['Crime_Type', 'Year', 'Area']
)

df.to_csv('crime_dataset.csv', index=False)

print("Crime Dataset Created Successfully")

print("\nFIRST 10 ROWS")
print(df.head(10))

print("\nDATASET INFORMATION")
print(df.info())

print("\nNULL VALUES")
print(df.isnull().sum())

print("\nSTATISTICAL SUMMARY")
print(df.describe())

sns.set(style="whitegrid")

plt.figure(figsize=(12,6))

sns.countplot(
    x='Crime_Type',
    data=df,
    order=df['Crime_Type'].value_counts().index
)

plt.title('Crime Count by Category')
plt.xlabel('Crime Type')
plt.ylabel('Count')

plt.xticks(rotation=45)

plt.show()

crime_counts = df['Crime_Type'].value_counts()

plt.figure(figsize=(10,10))

plt.pie(
    crime_counts,
    labels=crime_counts.index,
    autopct='%1.1f%%'
)

plt.title('Crime Distribution')

plt.show()

yearly_crime = df.groupby('Year').size()

plt.figure(figsize=(10,6))

yearly_crime.plot(
    marker='o',
    linewidth=3
)

plt.title('Year-wise Crime Trend')
plt.xlabel('Year')
plt.ylabel('Number of Crimes')

plt.grid(True)

plt.show()

plt.figure(figsize=(14,6))

sns.countplot(
    x='Area',
    data=df,
    order=df['Area'].value_counts().index
)

plt.title('Area-wise Crime Analysis')
plt.xlabel('Area')
plt.ylabel('Crime Count')

plt.xticks(rotation=45)

plt.show()

numeric_df = df.select_dtypes(include=np.number)

plt.figure(figsize=(6,4))

sns.heatmap(
    numeric_df.corr(),
    annot=True,
    cmap='coolwarm'
)

plt.title('Correlation Heatmap')

plt.show()

print("\nTOP CRIME TYPES")
print(df['Crime_Type'].value_counts().head(10))

plt.figure(figsize=(10,6))

sns.countplot(
    x='Year',
    data=df
)

plt.title('Crime Count Per Year')
plt.xlabel('Year')
plt.ylabel('Crime Count')

plt.show()

plt.figure(figsize=(14,8))

sns.countplot(
    x='Area',
    hue='Crime_Type',
    data=df
)

plt.title('Area vs Crime Type')

plt.xticks(rotation=45)

plt.show()

df.to_csv('cleaned_crime_dataset.csv', index=False)

print("\nPROJECT COMPLETED SUCCESSFULLY")
