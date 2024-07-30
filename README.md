# Home Sales Analysis

This project uses SparkSQL to determine key metrics about home sales data. The analysis involves creating temporary views, partitioning data, caching, and uncaching temporary tables to improve processing efficiency.

## Table of Contents
- [Installation and Setup](#installation-and-setup)
- [Usage Instructions](#usage-instructions)
- [Project Overview](#project-overview)
- [Dependencies](#dependencies)
- [Logic and Workflow](#logic-and-workflow)

## Installation and Setup

For this project, we recommend using **Google Colaboratory**. Follow these steps to set up your environment:

### Google Drive:
1. Open your browser and navigate to **drive.google.com**.
2. Create an account or sign in using your Google credentials.

### Google Colaboratory:
1. Once signed in to **Google Drive**, click on **+ New**, **More**, then **+ Connect more apps**.
2. Search for **Colaboratory** in the **Google Workspace Marketplace**.
3. Click on **Colaboratory** and follow the installation instructions.
4. After installation, you can launch **Google Colaboratory** from the **+ New** > **More** menu in **Google Drive**.

## Usage Instructions

The repository contains the following notebook:
- **Home_Sales.ipynb**: A Python script to be executed in **Google Colab**. 
This notebook reproduces the analysis steps described below.

To run the notebook:
1. Upload the **Home_Sales.ipynb** notebook to your Colab environment.
2. Execute the cells in the notebook sequentially.

## Project Overview

The goal of this project is to analyze home sales data using **SparkSQL** and **PySpark**. The dataset is sourced from an AWS S3 bucket:
[Home Sales Data](https://2u-data-curriculum-team.s3.amazonaws.com/dataviz-classroom/v1.2/22-big-data/home_sales_revised.csv)

Key tasks include:
- Calculating average home prices based on various criteria.
- Creating temporary views of the data.
- Partitioning the data using Parquet format.
- Caching and uncaching temporary tables to study their impact on query performance.

## Dependencies

Ensure the following dependencies are installed:
- **Java** (OpenJDK 11)
- **Spark** (version 3.4.1 or compatible)
- **findspark** (Python library)

These dependencies are installed within the notebook using the following commands:

```python
# Install Java
!apt-get update -qq
!apt-get install openjdk-11-jdk-headless -qq > /dev/null

# Install findspark
!pip install -q findspark

## Results:

# 3. What is the average price for a four bedroom house sold per year, rounded to two decimal places?

+----+---------+
|year| AvgPrice|
+----+---------+
|2022|296363.88|
|2019| 300263.7|
|2020|298353.78|
|2021|301819.44|
+----+---------+

# 4. What is the average price of a home for each year the home was built, that have 3 bedrooms and 3 bathrooms, rounded to two decimal places?

+----------+-------------+
|year_built|average_price|
+----------+-------------+
|      2010|    292859.62|
|      2011|    291117.47|
|      2012|    293683.19|
|      2013|    295962.27|
|      2014|    290852.27|
|      2015|     288770.3|
|      2016|    290555.07|
|      2017|    292676.79|
+----------+-------------+

# 5. What is the average price of a home for each year the home was built, that have 3 bedrooms, 3 bathrooms, with two floors, and are greater than or equal to 2,000 square feet, rounded to two decimal places?

+----------+-------------+
|year_built|average_price|
+----------+-------------+
|      2010|    285010.22|
|      2011|    276553.81|
|      2012|    307539.97|
|      2013|    303676.79|
|      2014|    298264.72|
|      2015|    297609.97|
|      2016|     293965.1|
|      2017|    280317.58|
+----------+-------------+

# 6. What is the average price of a home per "view" rating, rounded to two decimal places, having an average home price greater than or equal to $350,000?
# Order by descending view rating.
# Although this is a small dataset, determine the run time for this query.

+----+-------------+
|view|average_price|
+----+-------------+
|  99|   1061201.42|
|  98|   1053739.33|
|  97|   1129040.15|
|  96|   1017815.92|
|  95|    1054325.6|
|  94|    1033536.2|
|  93|   1026006.06|
|  92|    970402.55|
|  91|   1137372.73|
|  90|   1062654.16|
|  89|   1107839.15|
|  88|   1031719.35|
|  87|    1072285.2|
|  86|   1070444.25|
|  85|   1056336.74|
|  84|   1117233.13|
|  83|   1033965.93|
|  82|    1063498.0|
|  81|   1053472.79|
|  80|    991767.38|
+----+-------------+
only showing top 20 rows

--- 2.3178492759232478 seconds ---

# 9. Using the cached data, run the last query above, that calculates the average price of a home per "view" rating, rounded to two decimal places, having an average home price greater than or equal to $350,000.
# Determine the runtime and compare it to the uncached runtime.

+----+----------+
|view|  AvgPrice|
+----+----------+
|  99|1061201.42|
|  98|1053739.33|
|  97|1129040.15|
|  96|1017815.92|
|  95| 1054325.6|
|  94| 1033536.2|
|  93|1026006.06|
|  92| 970402.55|
|  91|1137372.73|
|  90|1062654.16|
|  89|1107839.15|
|  88|1031719.35|
|  87| 1072285.2|
|  86|1070444.25|
|  85|1056336.74|
|  84|1117233.13|
|  83|1033965.93|
|  82| 1063498.0|
|  81|1053472.79|
|  80| 991767.38|
+----+----------+
only showing top 20 rows

--- 0.8328479274212877 seconds ---


uncached table 	~ 2.32 seconds
cached table 	~ 0.83 seconds

# 13. Using the parquet DataFrame, run the last query above, that calculates
# the average price of a home per "view" rating, rounded to two decimal places,
# having an average home price greater than or equal to $350,000.
# Determine the runtime and compare it to the cached runtime.

+----+-------------+
|view|average_price|
+----+-------------+
|  99|   1061201.42|
|  98|   1053739.33|
|  97|   1129040.15|
|  96|   1017815.92|
|  95|    1054325.6|
|  94|    1033536.2|
|  93|   1026006.06|
|  92|    970402.55|
|  91|   1137372.73|
|  90|   1062654.16|
|  89|   1107839.15|
|  88|   1031719.35|
|  87|    1072285.2|
|  86|   1070444.25|
|  85|   1056336.74|
|  84|   1117233.13|
|  83|   1033965.93|
|  82|    1063498.0|
|  81|   1053472.79|
|  80|    991767.38|
+----+-------------+
only showing top 20 rows

--- 0.8059824002852082 seconds ---







