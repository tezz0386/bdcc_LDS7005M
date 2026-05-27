# Big Data Cloud Computing: NYC Taxi Analysis on Azure

This repository contains a Jupyter Notebook for processing and analysing NYC Yellow Taxi trip data using Microsoft Azure Blob Storage, Azure Databricks, Apache Spark, PySpark, Pandas, and Matplotlib.

The notebook file is:

```text
BDCC_Tejendra_dangaura.ipynb
```

## Project Overview

The notebook performs a full cloud-based big data workflow:

1. Reads NYC Yellow Taxi PARQUET files from Azure Blob Storage.
2. Converts the PARQUET files into CSV format.
3. Saves the converted CSV files back into Azure Blob Storage.
4. Cleans and preprocesses the CSV files using PySpark.
5. Generates cleaned CSV output files.
6. Describes the cleaned datasets.
7. Performs data analysis using Spark DataFrames.
8. Produces visual charts using Matplotlib.

## Dataset

The project uses NYC Yellow Taxi trip data for the following months:

```text
yellow_tripdata_2025-09.parquet
yellow_tripdata_2025-10.parquet
yellow_tripdata_2025-11.parquet
yellow_tripdata_2025-12.parquet
```

The source files should be stored inside the selected Azure Blob Storage container.

## Technologies Used

- Microsoft Azure Blob Storage
- Azure Databricks
- Apache Spark
- PySpark
- Python
- Pandas
- Matplotlib
- Jupyter Notebook

## Prerequisites

Before running the notebook, make sure you have:

1. An Azure Storage Account.
2. A Blob Storage container.
3. NYC Taxi PARQUET files uploaded to the container.
4. Azure Databricks workspace and cluster.
5. SAS token with suitable permissions.
6. Python libraries available in the Databricks environment.

The Spark configuration uses the following packages:

```text
org.apache.hadoop:hadoop-azure:3.3.6
com.microsoft.azure:azure-storage:8.6.6
```

## Important Security Note

Do not upload your real SAS token to GitHub.

In the notebook, replace the SAS token value with your own token before running the file:

```python
tezz_sas_token = "YOUR_SAS_TOKEN"
```

For GitHub submission, it is better to keep the SAS token hidden or load it from a secure secret store.

## Azure Folder Structure

The expected Azure Blob Storage structure is:

```text
nyc/
│
├── yellow_tripdata_2025-09.parquet
├── yellow_tripdata_2025-10.parquet
├── yellow_tripdata_2025-11.parquet
├── yellow_tripdata_2025-12.parquet
│
├── csv/
│   ├── yellow_tripdata_2025-09.csv
│   ├── yellow_tripdata_2025-10.csv
│   ├── yellow_tripdata_2025-11.csv
│   └── yellow_tripdata_2025-12.csv
│
└── clean_data/
    ├── yellow_tripdata_2025-09.csv
    ├── yellow_tripdata_2025-10.csv
    ├── yellow_tripdata_2025-11.csv
    └── yellow_tripdata_2025-12.csv
```

## How to Execute the Notebook

### Step 1: Upload the Dataset to Azure

Upload the four PARQUET files into your Azure Blob Storage container.

Example container name used in the notebook:

```text
nyc
```

### Step 2: Open the Notebook in Azure Databricks

Upload or import the notebook into Azure Databricks:

```text
BDCC_Tejendra_dangaura.ipynb
```

Attach the notebook to a running Databricks cluster.

### Step 3: Update Azure Configuration

Check and update these values in the notebook:

```python
tezz_storage_account = "your_storage_account_name"
tezz_container_name = "your_container_name"
tezz_sas_token = "YOUR_SAS_TOKEN"
```

### Step 4: Run PARQUET to CSV Conversion

Run the first code section.

This section reads the PARQUET files from Azure Blob Storage and converts them into CSV files.

Expected output:

```text
Single CSV file saved successfully at: wasbs://nyc@your_storage_account.blob.core.windows.net/csv/yellow_tripdata_2025-09.csv
Single CSV file saved successfully at: wasbs://nyc@your_storage_account.blob.core.windows.net/csv/yellow_tripdata_2025-10.csv
Single CSV file saved successfully at: wasbs://nyc@your_storage_account.blob.core.windows.net/csv/yellow_tripdata_2025-11.csv
Single CSV file saved successfully at: wasbs://nyc@your_storage_account.blob.core.windows.net/csv/yellow_tripdata_2025-12.csv
```

### Step 5: Run Data Preprocessing

Run the preprocessing section.

This section cleans the CSV files by:

- Removing duplicate rows.
- Removing rows with missing important values.
- Removing invalid trip distances.
- Removing invalid fare amounts.
- Removing invalid passenger counts.
- Calculating trip duration in minutes.
- Creating pickup hour, pickup day, and pickup month columns.
- Saving cleaned output into the `clean_data` folder.

Expected output:

```text
Reading CSV file from Azure: yellow_tripdata_2025-09.csv

Original Dataset Information
Rows Before Cleaning: ...
Columns: ...

Preprocessing Summary
Processed File: yellow_tripdata_2025-09.csv
Rows Before Cleaning: ...
Rows After Cleaning: ...
Removed Rows: ...
Cleaned File Saved At: wasbs://nyc@your_storage_account.blob.core.windows.net/clean_data/yellow_tripdata_2025-09.csv

Sample Cleaned Data
```

The same type of output is shown for all four selected months.

### Step 6: Describe Cleaned Datasets

Run the dataset description section.

Expected output includes:

- Total rows.
- Total columns.
- Column names.
- Dataset schema.
- Numerical summary statistics.
- Missing value count.
- First five sample records.

Example output:

```text
DATASET DESCRIPTION FOR: yellow_tripdata_2025-09.csv
Total Rows: ...
Total Columns: ...
Column Names:
- VendorID
- tpep_pickup_datetime
- tpep_dropoff_datetime
...
Dataset Schema:
root
 |-- VendorID: integer
 |-- tpep_pickup_datetime: timestamp
...
```

### Step 7: Run Data Analysis and Visualisation

Run the analysis and chart sections.

The notebook generates the following outputs:

1. Taxi Trip Demand by Pickup Hour
2. Taxi Trip Demand by Day of Week
3. Monthly Taxi Trip Trend
4. Top 10 Pickup Locations
5. Top 10 Drop-off Locations
6. Payment Method Distribution
7. Average Trip Distance by Pickup Hour
8. Average Trip Duration by Pickup Hour
9. Average Tip Amount by Payment Type

## Final Output of the Notebook

After successful execution, the notebook produces:

### 1. Converted CSV Files

Saved in:

```text
wasbs://<container>@<storage_account>.blob.core.windows.net/csv/
```

### 2. Cleaned CSV Files

Saved in:

```text
wasbs://<container>@<storage_account>.blob.core.windows.net/clean_data/
```

### 3. Dataset Summary

The notebook displays:

- Rows before cleaning.
- Rows after cleaning.
- Removed row count.
- Column names.
- Schema details.
- Summary statistics.
- Missing value counts.
- Sample records.

### 4. Visual Analysis Charts

The notebook displays charts for:

- Hourly trip demand.
- Weekly trip demand.
- Monthly trip trend.
- Pickup and drop-off location demand.
- Payment method distribution.
- Average distance by hour.
- Average duration by hour.
- Average tip by payment type.

## Expected Insights

The analysis helps identify:

- Peak taxi demand hours.
- Busy days of the week.
- Monthly trip trends.
- Popular pickup and drop-off locations.
- Most common payment methods.
- Average trip distance patterns.
- Average trip duration patterns.
- Tip behaviour by payment type.

## Common Issues and Fixes

### Issue: SAS Token Error

If Azure access fails, generate a new SAS token with read, write, create, delete, and list permissions.

### Issue: File Not Found

Check that the PARQUET file names exactly match the names used in the notebook.

### Issue: Azure Hadoop Package Error

Make sure the Databricks cluster can download these packages:

```text
org.apache.hadoop:hadoop-azure:3.3.6
com.microsoft.azure:azure-storage:8.6.6
```

### Issue: dbutils Not Found

This notebook is designed for Azure Databricks. The `dbutils` commands may not work in a normal local Jupyter Notebook without modification.

## Author

Tejendra Dangaura

## Project Title

Optimising Big Data Processing in the Cloud with Dataset Extraction and Analysis
