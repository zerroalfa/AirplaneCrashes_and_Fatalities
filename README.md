# AirplaneCrashes_and_Fatalities
this is my 1st project with Quantum Analytics

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Recommendations](#recommendations)

### Project Overview
---



**Project Overview: Airplane Crashes and Fatalities Analysis**  

This project focuses on analyzing the **Airplane Crashes and Fatalities dataset**, which provides comprehensive information on over 5,000 airplane crashes worldwide since 1948. The dataset includes key details such as:  

- **Date, time, and location** of the crash  
- **Operator and flight details** (e.g., flight number, route, aircraft type)  
- **Registration and aircraft identifiers** (e.g., registration number, cn/In number)  
- **Casualty details**, including fatalities on board and ground fatalities  
- A **summary of each accident**  

### Objectives:  
- **Explore Aviation Safety Trends**: Identify trends in airplane crashes over time, including geographic hotspots and patterns related to specific operators or aircraft types.  
- **Casualty Analysis**: Examine the impact of crashes on passengers and crew, as well as ground fatalities, to uncover factors contributing to higher fatality rates.  
- **Insights for Safety Improvement**: Analyze the dataset to provide insights into potential areas of improvement in aviation safety and risk mitigation.  

### Value of the Dataset:  
This dataset is a critical resource for:  
- **Aviation Safety Analysts**: Providing historical data for improving safety protocols.  
- **Data Enthusiasts**: Offering a robust platform for creating data visualizations and conducting exploratory analysis.  
- **Storytelling through Data**: Uncovering compelling narratives about aviation safety, historical incidents, and their impact on the industry.  

### Potential Use Cases:  
1. **Visualization of Crash Trends**: Create time-series visualizations to showcase crash frequency and fatalities by year.  
2. **Geographic Analysis**: Use location data to map crash sites and analyze regional trends.  
3. **Aircraft Type Analysis**: Compare crash rates across different aircraft models to assess safety records.  
4. **Sentiment Analysis**: Study accident summaries for recurring themes and contributing factors.  

This project will provide actionable insights, contributing to a deeper understanding of aviation safety and potentially influencing policy and training improvements within the aviation industry.

![Dashboard]![1 Airplane Crashes and Fatalities](https://github.com/user-attachments/assets/85aee65d-8a0c-4b79-b888-e4ac953c24e3)



### Data Sources

Airplane_Crashes_and_Fatalities dataset: The primary dataset used for this analysis is the "Airplane_Crashes_and_Fatalities.csv" file, containing detailed information about Airplane Crashes and Fatalities.

### Tools

- Excel - Data Cleaning
  - [Download here](https://microsoft.com)
- SQL Server - Data Analysis
- PowerBI - Creating reports


### Data Cleaning/Preparation

In the initial data preparation phase, we performed the following tasks:
1. Data loading and inspection.
2. Handling missing values.
3. Data cleaning and formatting.

### Exploratory Data Analysis

EDA involved exploring the sales data to answer key questions, such as:

- What is the overall sales trend?
- Which products are top sellers?
- What are the peak sales periods?

### Data Analysis

Include some interesting code/features worked with

**SQL Schema for the Dataset**


```sql
CREATE TABLE Airplane_Crashes (
    Index INT,
    Date DATE,
    Time VARCHAR(10),
    Location VARCHAR(255),
    Operator VARCHAR(255),
    Flight_No VARCHAR(50),
    Route VARCHAR(255),
    Type VARCHAR(255),
    Registration VARCHAR(50),
    CN_IN VARCHAR(50),
    Aboard INT,
    Fatalities INT,
    Ground INT,
    Summary TEXT,
    Year INT,
    Month INT
);

```

 **Total In-Flight Fatalities, Ground Fatalities, Total Crashes, Total Fatalities, and Fatality Ratio per Flight**
```sql
SELECT 
    SUM(Fatalities) AS Total_In_Flight_Fatalities,
    SUM(Ground) AS Total_Ground_Fatalities,
    COUNT(*) AS Total_Crashes,
    SUM(Fatalities + Ground) AS Total_Fatalities,
    AVG(CAST(Fatalities AS FLOAT) / NULLIF(Aboard, 0)) AS Fatality_Ratio_Per_Flight
FROM Airplane_Crashes;
```
**Total Crashes by Route**
```sql
SELECT 
    Route, 
    COUNT(*) AS Total_Crashes
FROM Airplane_Crashes
WHERE Route IS NOT NULL
GROUP BY Route
ORDER BY Total_Crashes DESC;
```
**Trend Over Time**
```sql
SELECT 
    Year, 
    COUNT(*) AS Total_Crashes, 
    SUM(Fatalities + Ground) AS Total_Fatalities
FROM Airplane_Crashes
GROUP BY Year
ORDER BY Year ASC;
```
**Aircraft Type Involved in the Most Crashes**
```sql
SELECT 
    Type, 
    COUNT(*) AS Total_Crashes
FROM Airplane_Crashes
WHERE Type IS NOT NULL
GROUP BY Type
ORDER BY Total_Crashes DESC
LIMIT 1;
```
**Patterns in Where/When Crashes Occur**
```sql
SELECT 
    Location, 
    Month, 
    COUNT(*) AS Total_Crashes
FROM Airplane_Crashes
WHERE Location IS NOT NULL
GROUP BY Location, Month
ORDER BY Total_Crashes DESC;
```
**Most Common Operators**
```sql
SELECT 
    Operator, 
    COUNT(*) AS Total_Crashes
FROM Airplane_Crashes
WHERE Operator IS NOT NULL
GROUP BY Operator
ORDER BY Total_Crashes DESC
LIMIT 10;
```
**Frequency of Crashes by Month Over the Years**
```sql
SELECT 
    Month, 
    COUNT(*) AS Total_Crashes
FROM Airplane_Crashes
GROUP BY Month
ORDER BY Month ASC;
```

### Results/Findings

The analysis Results/Findings based on the SQL analysis outcomes:

**Total Fatalities and Fatality Ratios**
Total In-Flight Fatalities: The total number of fatalities aboard aircraft highlights the human cost of these accidents.
Total Ground Fatalities: Accidents have caused additional casualties among people on the ground.
Fatality Ratio per Flight: The average fatality ratio per flight indicates how severe crashes tend to be.
Key Findings:
A significant proportion of crashes result in fatalities for most passengers on board, suggesting that crash survivability is limited, especially in earlier years.

**Total Crashes by Route**
Routes with the highest crash frequencies can be identified.
Key Findings:
Common routes or flight paths may have specific geographic or environmental challenges, such as adverse weather, mountainous terrain, or high air traffic.

**Trend Over Time**
Crashes per Year: By analyzing yearly trends, we observe spikes in crashes during specific periods.
Key Findings:
Aviation safety has improved over time, as the frequency of crashes appears to decline in more recent decades.
Specific historical periods (e.g., wartime years) show higher crash frequencies due to increased flight activity and possibly lower safety standards.

**Aircraft Type Involved in Most Crashes**
Certain aircraft models/types are more frequently involved in crashes.
Key Findings:
Older aircraft models or those used heavily during early aviation history are more prone to crashes, suggesting advancements in technology and maintenance over time.

**Patterns in Location and Time**
Location Patterns: Some locations experience repeated crashes, possibly due to operational challenges, geographic features, or traffic density.
Seasonal Patterns: Certain months may have higher crash rates.
Key Findings:
Crashes show a regional concentration in areas with complex geography or weather-related risks (e.g., storms, snow, fog).
Seasonal increases could align with weather patterns or holiday travel surges.

**Most Common Operators**
Operators with the highest number of crashes are identified.
Key Findings:
A few operators have a disproportionately high number of crashes, potentially reflecting safety protocol differences, fleet age, or operational challenges.

**Frequency of Crashes by Month Over the Years**
Monthly trends reveal periods of higher accident frequencies.
Key Findings:
Certain months show higher crash rates, possibly linked to seasonal weather changes, visibility issues, or high travel demand.

**General Observation:**
The dataset highlights the evolution of aviation safety over time, showing clear improvements in crash rates, operator protocols, and aircraft reliability.
### Recommendations

Based on the analysis, we recommend the following actions:

**Focus on High-Risk Routes:**

Authorities and airlines should prioritize improving safety protocols on routes with higher crash frequencies.

**Enhanced Monitoring of Specific Aircraft Types:**

Aircraft models with frequent crashes should undergo stringent inspections and reviews.

**Safety Measures for Seasonal Risks:**

Specific months showing higher crash frequencies might require improved weather prediction and pilot training for adverse conditions.

**Strengthen Operator Safety Standards:**

Frequent crashes by certain operators call for stricter regulatory oversight and operational audits.

**Public Awareness:**

Sharing findings about safety and fatality ratios with the public can enhance trust and inform passengers about air travel risks.


### Limitations

**Incomplete Data:**

Missing values in key columns (e.g., Time, Route, Fatalities) may impact the accuracy of findings.

**Historical Context:**

Changes in aviation technology, regulations, and reporting standards over time may skew trends.

**Lack of Causal Data:**

The dataset lacks detailed cause analysis, making it hard to determine specific crash reasons.

**Operator and Aircraft Identification:**

Variations in naming and missing entries for operators and aircraft types could reduce the precision of analysis.

### Observations During Data Cleaning

The dataset has been cleaned, and the following columns contain missing values:

Time: 2219 missing.
Location: 20 missing.
Operator: 18 missing.
Flight #: 4199 missing.
Route: 1706 missing.
Type: 27 missing.
Registration: 335 missing.
cn/In: 1228 missing.
Aboard: 22 missing.
Fatalities: 12 missing.
Ground: 22 missing.
Summary: 390 missing.


