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
