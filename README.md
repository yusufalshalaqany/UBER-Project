# 📊 UBER Project

 <a href="https://app.powerbi.com/view?r=eyJrIjoiYzk5ZmY2YmMtODFhYS00ODExLWI1ZGQtY2U0ZTBiYWUwMGFjIiwidCI6IjJiYjZlNWJjLWMxMDktNDdmYi05NDMzLWMxYzZmNGZhMzNmZiIsImMiOjl9">
 <img src="https://img.shields.io/badge/View%20A%20Project-%23FFED00?style=for-the-badge">
     </a>
 <a href="https://www.linkedin.com/posts/yusuf-al-shalaqany_dataanalysis-python-pandas-activity-7375628745493258240-LVYS?utm_source=share&utm_medium=member_desktop&rcm=ACoAAC_Cv7UBLUQanl94PAQobXd5FF9DsRZeNnc">
 <img src="https://img.shields.io/badge/LinkedIn%20Post-%232480E6?style=for-the-badge">

 <br />

# Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Preparation](#data-preparation)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Key Learning](#key-learning)

### Project Overview

This data analysis project aims to provide insights about UBER trips and performance from 2020 to 2025. By analyzing various aspects of the trips data, we seek to identify trends, make data-driven recommendations, and gain a deeper understanding of UBER performance.

### Data Sources

UBER Dataset: The primary dataset used for this analysis is the "UBERDataset.csv" file, containing detailed information about each trip.
  - [Download from attachments](https://github.com/yusufalshalaqany/UBER-Project/blob/main/Data%20Source/UBERDataset.csv)

 <br />

### Tools

1 - Applications
- Anaconda (Jupyter Notebook) - Data Exploration and Cleaning by Python/Pandas
  - [Download here](https://www.anaconda.com/)
- PowerBI - Creating reports
  - [Download here](https://www.microsoft.com/en-us/power-platform/products/power-bi/downloads)

 <br />
  
2 - Desing 
- [Figma](https://www.figma.com): Help me to create an organized background for dashboard

 <br />

### Data Preparation

Python (By using Pandas): Explore and cleaning the data, I focused on three things: -

1 - Data Understanding (Types, measures and each column meaning)

2 - Check duplication and null values and replace them with suitable values by:

  - Replace all null values in Stop Location with "Unknown" and in Purpose with "Other"
  - Replace all null values in Driver Rating with the median value after checking outliers.

 <br />

### Data Analysis

- **Include some interesting code/features worked with Python**

1 - Import Pandas
```python
import pandas as pd
```
2 - Import Uber Dataset Dataset & Read it
```python
df = pd.read_csv("UBERDataset.csv")
df.info()
pd.set_option("display.max_columns", None) 
df.head(20)
```
3 - Check Duplicated Values
```python
print(df.duplicated().sum())
```
4 - Check Null Values
```python
print(df.isnull().sum())
```
5 - Fill Null Values with A Suitable Values
```python
df.fillna({"STOP":"Unknown"}, inplace = True)
df.fillna({"PURPOSE":"Other"}, inplace = True)
```
6 - Get Outliers then Fill Null Values with A Suitable Values with 2 ways
```python
q1 = df["DRIVER_RATING"].quantile(0.25)
q3 = df["DRIVER_RATING"].quantile(0.75)

iqr = q3 - q1

lower_bond = q1 - (1.5 * iqr)
upper_bond = q3 + (1.5 * iqr)

outliers = df[((df["DRIVER_RATING"] < lower_bond) | (df["DRIVER_RATING"] > upper_bond))]

outliers.count()
```
7 - 1st Way: Fill Null Values with Median
```python
print(df["DRIVER_RATING"].median())
df.fillna({"DRIVER_RATING":df["DRIVER_RATING"].median()}, inplace = True)
```
8 - 2nd Way: Remove Null Values with Update Dataframe Range
```python
df = df[((df["DRIVER_RATING"] > lower_bond) & (df["DRIVER_RATING"] < upper_bond))]
```
9 - Export Cleaned CSV File
```python
df.to_csv('Cleaned_uber_dataset.csv', index=False)
```

 <br />

- **Power BI: Data modeling, DAX measures, and building interactive dashboards**

Data Modeling:
- Make a star schema to improve analysis performance

DAX Measures:
```dax
Average Fare = AVERAGE(UBERFact[Fare Amount])
```
```dax
Average Rate = AVERAGE(UBERFact[Driver Rating])
```
```dax
Fare Amount = SUM(UBERFact[Fare Amount])
```
```dax
Maximum Fare = MAX(UBERFact[Fare Amount])
```
```dax
Miles = SUM(UBERFact[Miles])
```
```dax
Minimum Fare = MIN(UBERFact[Fare Amount])
```
```dax
Passengers = SUM(UBERFact[No. Passenger])
```
```dax
Regions = DISTINCTCOUNT(UBERFact[StartLocationID])
```
```dax
Trips = SUM(UBERFact[TripID])
```

Reporting:
1. Make a star schema to improve analysis performance
2. Make a dimension for Date using a simple M language code
```m
let
	StartDate = #date(2020, 01, 01),
	EndDate = #date(2025, 04, 03),
	NumberOfDays = Duration.Days(EndDate - StartDate) + 1,
	Dates = List.Dates(StartDate, NumberOfDays, #duration(1, 0, 0, 0))
in
	Dates
```
3. Make 4 reports to get valuable insights from data

 <br />

### Results

- Trips Report: 
  - The trips distrebution by year, the largest number of trips in 2021.
  - The most trip type is round (to a place and back usually over the same route).
  - Most trips purposes for entertain or commute.

- Fare Report:
  - The fare amount distrebution by year, the largest number of fare in 2021.
  - The most fare for personal trips and were payed by credit card.

- Cars Report:
  - The most fare for trips by economy cars.

- Region Report:
  - Top region is Shannon City "North America" by number of trips 
  - Top region is South Katherine "Australia" by total fare amount

### Key Learning

💡 Combining Python for heavy data processing with Power BI for interactive dashboards creates a powerful working.
