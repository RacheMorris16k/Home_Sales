# Home_Sales
# 🏡 Home Sales Data Analysis with PySpark

This project uses PySpark to analyze a home sales dataset. It demonstrates key Spark features such as creating temporary views, running SQL queries, caching tables, and exporting partitioned Parquet files.

---
Home_Sales/
├── Home_Sales.ipynb # Main notebook with PySpark code
├── home_sales_revised.csv # Input CSV dataset
├── home_sales_partitioned/ # Output Parquet folder (created by write step)
└── README.md # This file

## 📊 Dataset Overview

**File:** `home_sales_revised.csv`  
**Columns:**
- `id` – unique ID
- `date` – sale date
- `date_built` – year home was built
- `price` – sale price
- `bedrooms`, `bathrooms` – number of rooms
- `sqft_living`, `sqft_lot` – size of home and lot
- `floors` – number of floors
- `waterfront` – binary flag for waterfront property
- `view` – view score (0-100)

---

## 🧪 Key Tasks

### 1. **Spark Setup**
- Set environment variables for Spark, Java, and Hadoop.
- Verified with:
  ```bash
  java -version
  pyspark --version

### 2. Load CSV into Spark DataFrame
df = spark.read.csv("home_sales_revised.csv", header=True, inferSchema=True)

### 3. Create a Temporary View
df.createOrReplaceTempView("home_sales")

### 4. Run SQL Queries
Average price for 4-bedroom homes by year.

Average price for 3 bed / 3 bath homes by year built.

Prices for large homes (≥ 2000 sqft).

View score and prices for expensive homes.

### 5. Cache Table
spark.catalog.cacheTable("home_sales")

### 6. Compare Query Speeds
Used time.time() to compare cached vs. uncached query runtimes.

### 7. Partition by date_built and Export Parquet
df.filter(df["date_built"].isNotNull()) \
  .write.partitionBy("date_built") \
  .mode("overwrite") \
  .parquet("home_sales_partitioned")

✅ Environment Setup
Set up environment variables in your notebook:

import os

os.environ["JAVA_HOME"] = r"C:\Program Files\Java\jdk-11"
os.environ["HADOOP_HOME"] = r"C:\spark-3.5.5-bin-hadoop3"
os.environ["PATH"] += os.pathsep + r"C:\spark-3.5.5-bin-hadoop3\bin"

### Initialize findspark and create a session:
# Import packages
from pyspark.sql import SparkSession
from pyspark.sql.functions import avg, round
import time

try:
    spark.stop()
except:
    pass
# Create a SparkSession
spark = SparkSession.builder.appName("SparkSQL").getOrCreate()
#Show SparkSession
spark

⚙️ Requirements
Python 3.12+

Java 11 

Apache Spark 3.3.1 with Hadoop 3.x

PySpark

winutils.exe (Windows only)

VSCode or Jupyter Notebook

🛠 Troubleshooting
Partitioning Errors: Check for Java/Hadoop misconfigurations, or missing winutils.exe.

Permissions: Run VSCode or Jupyter as administrator and make sure folder access is not blocked.

Controlled Folder Access: Disable it in Windows Security (under Ransomware Protection).

Empty Output Folder: Ensure the path exists and no .parquet() error occurred.


