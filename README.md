# Microsoft Fabric's Spark Data Exploration

This repository provides a code snippet to perform quick data exploration using Microsoft Fabric's Spark. The code demonstrates how to ingest data, perform basic analysis, and visualize the results. Follow the instructions below to set up and run the code.

## Setup

1. Read More About Microsoft Fabric and Apache Spark Here:
    - [Microsoft Fabric Apache Spark](https://learn.microsoft.com/en-us/training/modules/use-apache-spark-work-files-lakehouse/4-dataframe)
    - [Microsoft Fabric](https://fabric.microsoft.com/)

2. Clone this repository:

   ```bash
   git clone https://github.com/gbengaayelab/ApacheSparkExplorationFabric.git
   ```

## Code

Open `Notebook 1` and run the following code:

```python
# Welcome to your new notebook
# Type here in the cell editor to add code!
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import pyspark.sql.functions as F
import pyspark.sql.types as T

df = spark.sql("SELECT * FROM lakehouse_1_lab.sales LIMIT 1000")

df.columns

display(df.describe())

display(df.summary())

# Convert the 'OrderDate' column to a date type
df = df.withColumn('OrderDate', F.to_date('OrderDate').cast(T.DateType()))

# Group the data by 'OrderDate' and calculate the sum of 'TaxAmount' and 'UnitPrice'
grouped_df = df.groupBy('OrderDate').agg(F.sum('TaxAmount').alias('TaxAmount'), F.sum('UnitPrice').alias('Price'))

# Convert the DataFrame to Pandas DataFrame for plotting
pandas_df = grouped_df.toPandas()

# Plotting the data
plt.plot(pandas_df['OrderDate'], pandas_df['TaxAmount'], label='Tax')
plt.plot(pandas_df['OrderDate'], pandas_df['Price'], label='Price')
plt.legend()
plt.title('Price and Tax Amount Relationship to Order Date')
plt.ylabel('TaxAmount and Price')
plt.xlabel('Order Date')
plt.show()

pandas_df.plot(x='OrderDate', y='TaxAmount', label='Tax', kind='line')
plt.legend()
plt.title('Tax Amount Relationship to Order Date')
plt.ylabel('TaxAmount')
plt.xlabel('Order Date')
plt.show()

pandas_df.plot(x='OrderDate', y='Price', label='Price', kind='line')
plt.legend()
plt.title('Price Relationship to Order Date')
plt.ylabel('Price')
plt.xlabel('Order Date')
plt.show()
```

## Usage

1. Ensure you have set up Microsoft Fabric and have the necessary credentials.

2. Replace `lakehouse_1_lab.sales` in the code with your own dataset or table name OR better still, create a 'lakehouse_1_lab Fabric Lakehouse.

3. Run the code to perform data exploration and generate visualizations based on your data.

## Feedback and Support

If you encounter any issues or have any feedback, please [open an issue](https://github.com/gbengaayelab/ApacheSparkExplorationFabric.git/issues) in this repository.

For general support and questions, you can read the offcial Microsoft Fabric Apache Spark Documentation for assistance here: https://learn.microsoft.com/en-us/training/modules/use-apache-spark-work-files-lakehouse/4-dataframe.

---

Happy exploring and analyzing data with Microsoft Fabric's Spark!
```

Feel free to copy and paste the above Markdown content into your README file on GitHub. Let me know if there's anything else I can help you with!