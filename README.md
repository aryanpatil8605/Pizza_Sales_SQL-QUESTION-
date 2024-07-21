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
