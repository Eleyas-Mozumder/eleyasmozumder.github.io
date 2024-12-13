# Titanic Dataset Analysis 

## Table of Contents 

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Result/ Findings](#result-findings)


### Project Overview

This project focuses on exploring the Titanic dataset using SQL and creating a dynamic dashboard to visualize the insights. The analysis is designed for beginner-level SQL practitioners and demonstrates the process of data cleaning, querying, and visualization development. This project highlights key data trends such as survival rates, demographic influences, and ticket pricing patterns, providing a comprehensive understanding of the Titanic dataset.

### Data Sources

The Titanic dataset from Kaggle, specifically the train.csv file, serves as the primary source of analysis. This dataset includes information about passengers such as survival status, age, gender, ticket and class.

### Tools

- SQL Server - Data Analysis
- Power BI - Creating Reports

### Data Cleaning / Preparation

In the initial data preparation phase, I performed the following tasks:

1. Import Data into BigQuery
2. Create a new BigQuery project
3. Data Cleaning
4. Handle any missing values
5. Validate Data
6. Ensure data types are correct

### Exploratory Data Analysis

Answer the following questions using SQL queries in BigQuery:

- What percentage of passengers survived?
- What is the survival rate for each passenger class (1st, 2nd, 3rd)?
- What is the survival rate based on gender?
- What is the average fare for survivors vs. non-survivors?
- What is the average age of survivors and non-survivors?
- What is the survival rate based on the port of embarkation (C = Cherbourg, Q = Queenstown, S = Southampton)?
- How does family size (sum of SibSp and Parch) affect survival?
-  Who are the top 10 passengers who paid the highest fare and survived?
  
### Data Analysis 

Include some interesting code/ Features worked with

``` SQL

SELECT
  Round (COALESCE (Age, (
      SELECT
        AVG(Age)
      FROM
        `titanic-dataset-analysis.Dataset_Analysis.Train`
      WHERE
        Age IS NOT NULL))) AS Age,
  COALESCE(Fare, (
    SELECT
      AVG(Fare)
    FROM
      `titanic-dataset-analysis.Dataset_Analysis.Train`
    WHERE
      Fare IS NOT NULL)) AS Fare,
  COALESCE(Embarked, 'S') AS Embarked
  -- Assuming 'S' IS the most common value *
FROM
  `titanic-dataset-analysis.Dataset_Analysis.Train`; 
```


``` SQL

SELECT
  Sex,
  (SUM(Survived) / COUNT(*)) * 100 AS survival_rate
FROM
  `titanic-dataset-analysis.Dataset_Analysis.Train`
GROUP BY
  Sex
ORDER BY
  survival_rate DESC 
```


```SQL
SELECT
  Name,
  Round (Fare),
  Survived
FROM
  `titanic-dataset-analysis.Dataset_Analysis.Train`
WHERE
  Survived = 1
ORDER BY
  Fare DESC
LIMIT
  10
```

### Result/ Findings

The analysis of the Titanic dataset reveals key survival trends based on class, gender, age, and socio-economic factors. Overall, only 38.38% of passengers survived, with 1st-class passengers (62.96%) and females (74.20%) having the highest survival rates, highlighting socio-economic and gender priorities during evacuation. Younger passengers and those with smaller family sizes were more likely to survive, while passengers embarking from Cherbourg had the highest survival rate among ports. Economic inequality is evident as higher fares and 1st-class status strongly correlated with survival. These insights, supported by SQL analysis and visualizations, provide a comprehensive understanding of the disaster.


### Limitations 

The project has several limitations, including the incomplete and imbalanced nature of the Titanic dataset, such as missing values in critical fields like `Age` and `Cabin`, which may skew analysis results. The dataset primarily represents a specific historical context, limiting its generalizability to broader socio-economic studies. Additionally, assumptions made during data cleaning (e.g., imputation methods) and relying on SQL for analysis may oversimplify complex relationships within the data. Finally, the project does not account for potential biases or external factors, such as cultural norms, which could further influence survival outcomes.

 



