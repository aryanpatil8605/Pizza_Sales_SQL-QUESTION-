# Data Analysis Projects

This repository contains several data analysis projects that showcase skills in SQL, Power BI, Python (Pandas, NumPy), and R. Follow the instructions below to replicate each project.

## Project 1: Sales Analysis and Reporting

**Objective:** Analyze sales data to identify trends and patterns to support strategic decision-making.

### Data Collection

- **Data Source:** `sales_data.csv`
- **Sample Data:**

    ```plaintext
    Date,Product,Region,Sales
    2024-01-01,Widget A,North,1000
    2024-01-01,Widget B,South,1500
    2024-01-02,Widget A,North,1200
    2024-01-02,Widget B,South,1700
    ```

### Data Cleaning

**Python (Pandas):**

```python
import pandas as pd

# Load data
df = pd.read_csv('sales_data.csv')

# Display the first few rows
print(df.head())

# Check for missing values
print(df.isnull().sum())

# Fill or drop missing values if any
df = df.dropna()
```

### Data Analysis
**SQL (SQLite Example):**

```-- Create a table
CREATE TABLE sales (
    Date DATE,
    Product TEXT,
    Region TEXT,
    Sales INTEGER
);

-- Import data into the table
.mode csv
.import sales_data.csv sales

-- Query total sales by product
SELECT Product, SUM(Sales) AS TotalSales
FROM sales
GROUP BY Product;
```

### Data Visualization
**Power BI:**

1. Load `sales_data.csv` into Power BI.
2. Create the following visualizations:
   - **Bar Chart:** Total sales by product.
   - **Line Chart:** Sales trends over time.
   - **Slicer:** Filter data by region or product.

### Reporting
**Sales Analysis Report:**
**Sales Analysis Report**

- **Total Sales by Product:** Widget A: $2200, Widget B: $3200
- **Sales Trends:** Sales for Widget A and B have increased over the period.
- **Recommendations:** Focus on expanding sales efforts for Widget B in the North region.
