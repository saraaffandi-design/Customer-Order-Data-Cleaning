# Customer-Order-Data-Cleaning
Data cleaning and quality assessment of a messy customer orders dataset using Python and pandas.

## Business Problem

Businesses rely on accurate customer and order data to support sales reporting, customer analysis, and operational decision-making. However, data collected from different sources can contain duplicate records, missing values, inconsistent formats, and invalid values.

This project simulates a data quality improvement task for a company that wants to prepare its customer order data for downstream analysis.

The objective was to identify data quality issues, apply appropriate cleaning and validation rules, and produce a consistent dataset that can be used for further analysis and reporting.

### Business Questions

The cleaning process focused on the following questions:

- Are there duplicate order records?
- Are there missing or invalid values?
- Are categorical values represented consistently?
- Are dates stored in a consistent format?
- Are numerical values valid?
- Are order quantities reasonable?
- Are total amounts internally consistent?
- Is the final dataset suitable for downstream analysis?

---

# Data

The dataset contains customer order information, including customer, product, transaction, and return-related attributes.

The raw dataset contained **51,000 records** and **12 columns**. After duplicate removal, the working dataset contained **50,000 records**.

### Main Variables

| Column | Description |
|---|---|
| `customer_id` | Customer identifier |
| `country` | Customer's country |
| `category` | Product category |
| `product` | Product purchased |
| `quantity` | Quantity ordered |
| `unit_price` | Price per unit |
| `total_amount` | Total order amount |
| `order_date` | Date of the order |
| `status` | Order status |
| `payment_method` | Payment method |
| `is_returned` | Return indicator |

### Tools

- Python
- Pandas
- NumPy
- Jupyter Notebook
- VS Code
- Data Profiling

---

## Data Quality Issues

Initial profiling identified several data quality issues:

- Duplicate records
- Missing values
- Inconsistent categorical values
- Inconsistent Boolean representations
- Mixed date formats
- Invalid or negative quantities
- Missing unit prices
- Missing total amounts
- Inconsistent total amounts

  <img width="1782" height="782" alt="Screenshot 2026-09-27 111532" src="https://github.com/user-attachments/assets/45e7b1cf-89e9-474e-b1bc-25e69250ffe1" />

---

# Data Cleaning Process

The cleaning process was performed using Python and Pandas.

## 1. Duplicate Removal

Duplicate records were identified and removed from the dataset.

| Metric | Result |
|---|---:|
| Initial records | 51,000 |
| Duplicate records removed | 1,000 |
| Records after deduplication | 50,000 |

---

## 2. Categorical Standardisation

Categorical variables were standardised to ensure that equivalent values were represented consistently.

The cleaning process covered fields such as:

- Country
- Product category
- Order status
- Payment method

This reduces the risk of treating different representations of the same category as separate values during analysis.

---

## 3. Boolean Standardisation

Boolean values were represented using different formats in the raw data, including values such as:

- `TRUE`
- `True`
- `1`
- `Y`
- `No`
- `False`

These representations were mapped into a consistent Boolean format.

---

## 4. Quantity Validation

Quantity values were checked for zero and negative values.

Negative quantities were investigated before applying a transformation. They were not automatically classified as returns because the relationship between negative quantities and the return indicator was not fully consistent.

An audit flag was therefore retained before converting invalid quantities into valid positive values.

---

## 5. Date Standardisation

The raw dataset contained multiple date formats, including:

16/10/2022
07-27-2022
2024-01-04
18 Mar 2024
October 13, 2023

A format-specific parsing approach was used to correctly interpret the different date representations.

###Validation

| Check          | Result |
| -------------- | -----: |
| Unparsed dates |      0 |


All order dates were successfully converted into a consistent date format.

## 6. Unit Price Cleaning

Missing unit prices were investigated using information available within the order records.

Where appropriate, an implied unit price was calculated using:

total_amount / quantity

The resulting values were checked against plausible price ranges before being used for imputation.

This approach was used to reduce the risk of introducing implausible values into the cleaned dataset.

## 7. Total Amount Validation

The relationship between quantity, unit_price, and total_amount was investigated.

The analysis showed that the original total_amount values were not consistently aligned with:

quantity × unit_price

Therefore, the final dataset applies the following defined business rule:

total_amount = quantity × unit_price

This ensures that the final dataset has an internally consistent relationship between quantity, unit price, and total amount.

Important: This calculation is a defined cleaning rule rather than a guaranteed recovery of the original transaction amount.

# Results

## Data Quality Improvement

The cleaning workflow improved the overall consistency of the dataset.

| Data Quality Metric          | Before Cleaning | After Cleaning |
| ---------------------------- | --------------: | -------------: |
| Records                      |          51,000 |         50,000 |
| Duplicate records            |           1,000 |              0 |
| Missing values               |         Present |              0 |
| Invalid quantities           |         Present |              0 |
| Unparsed dates               |         Present |              0 |
| Missing unit prices          |         Present |              0 |
| Missing total amounts        |         Present |              0 |
| Total amount inconsistencies |         Present |              0 |

## Final Data Quality
After cleaning and validation, the dataset contained:

| Data Quality Check      | Final Result |
| ----------------------- | -----------: |
| Records                 |       50,000 |
| Duplicate records       |            0 |
| Missing values          |            0 |
| Quantity ≤ 0            |            0 |
| Negative total amounts  |            0 |
| Unparsed dates          |            0 |
| Missing unit prices     |            0 |
| Missing total amounts   |            0 |
| Total amount mismatches |            0 |

<img width="1905" height="782" alt="image" src="https://github.com/user-attachments/assets/bee8601b-a6a8-4259-9a5f-0bedaa6067ef" />


## Data Profiling

Data profiling was performed before and after the cleaning process to assess the overall data quality.

### Initial Data Profile

The initial profiling report was used to investigate:

- Missing values
- Duplicate records
- Data types
- Unique values
- Value distributions
- Potential data quality issues

[View Initial Profiling Report](https://chatgpt.com/g/g-p-6aad481c5cfc819194b009fe0c623b2c/c/initial_profiling_report.html)

### Cleaned Data Profile

A second profiling report was generated after cleaning to validate the final dataset.

[View Cleaned Profiling Report](https://chatgpt.com/g/g-p-6aad481c5cfc819194b009fe0c623b2c/c/cleaned_profiling_report.html)

## Key Results

The cleaning workflow transformed the original dataset into a consistent analysis-ready dataset.

The main improvements were:

- Reduced the dataset from 51,000 to 50,000 records after removing duplicates.
- Standardised categorical and Boolean values.
- Converted mixed date formats into a consistent format.
- Resolved invalid quantity values.
- Addressed missing unit prices and total amounts.
- Applied a consistent rule for calculating total amounts.
- Validated the final dataset using automated data quality checks.

# Key Takeaways

The project demonstrates that data cleaning requires more than simply removing missing values and duplicates.

Several issues required investigation before a cleaning rule could be applied.

For example, negative quantities could not automatically be treated as returns because the available return indicator did not consistently support this assumption.

Similarly, the original total_amount values did not consistently follow the expected relationship between quantity and unit price. The final total amounts were therefore recalculated using a defined business rule rather than assuming that the original values were correct.

The final validation showed that the cleaned dataset contained:

- 50,000 records
- 0 duplicate records
- 0 missing values
- 0 invalid quantities
- 0 unparsed dates
- 0 missing unit prices
- 0 missing total amounts
- 0 total amount mismatches


The cleaned dataset is now structured for downstream analysis and reporting.

# Next Steps & Limitations

## Next Steps

The cleaned dataset can be used as a foundation for further analysis, including:

- Sales performance analysis
- Revenue analysis
- Product category analysis
- Customer behaviour analysis
- Return analysis
- Customer segmentation
- Sales dashboard development

A natural next step would be to use the cleaned dataset to develop an interactive dashboard and investigate sales and customer trends.

## Limitations

### 1. Imputed Values

Some missing values required imputation based on information available within the dataset. Therefore, the imputed values may not exactly represent the original values.

### 2. Negative Quantities

Negative quantities required interpretation because they did not consistently correspond with the return indicator.

### 3. Total Amount Reconstruction

The final total_amount values were calculated using:

quantity × unit_price

This ensures mathematical consistency but does not guarantee that the calculated value represents the original transaction amount.

### 4. Practice Dataset

This dataset is used for portfolio and learning purposes. Therefore, the results should not be interpreted as actual company performance.

# Project Structure

Customer-Order-Data-Cleaning/
│
├── README.md
├── .gitignore
│
├── messy_customer_orders.csv
├── cleaned_customer_orders.csv
│
├── customer_orders_data_cleaning.ipynb
│
├── initial_profiling_report.html
└── cleaned_profiling_report.html

# Technologies

Python · Pandas · NumPy · Jupyter Notebook · VS Code · Data Profiling

## How to Run

### 1. Clone the Repository

Clone the repository to your local machine:

git clone https://github.com/saraaffandi-design/Customer-Order-Data-Cleaning.git

Navigate to the project folder:

cd Customer-Order-Data-Cleaning

### 2. Install the Required Libraries

Make sure Python is installed, then install the required libraries:

pip install pandas numpy jupyter ydata-profiling

### 3. Open the Project in VS Code

Open the Jupyter Notebook:

data_cleaning2.ipynb

Select a Python kernel and run the notebook from the beginning.

### 4. Input Data

The notebook uses the raw dataset:

messy_orders.csv

### 5. Output

After running the notebook, the cleaned dataset and data quality outputs are generated.

The project includes:

cleaned_orders.csv
data_quality_exceptions.csv

# 👩‍💻 Author
Siti Sarah Binti Mohd Affandi

MSc Operational Research and Analytics

Aspiring Data Analyst

# GitHub:
[https://github.com/saraaffandi-design](https://github.com/saraaffandi-design)
