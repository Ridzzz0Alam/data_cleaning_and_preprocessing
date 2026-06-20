# Data Cleaning & Preprocessing Assignment

A complete Jupyter Notebook that identifies and fixes 15 real-world data quality problems in a messy employee dataset using Python, pandas, and numpy.

## Dataset Overview

| Detail | Value |
|--------|-------|
| **File** | `dirty_dataset.xlsx` |
| **Rows** | 20,300 |
| **Columns** | 15 |
| **Source** | Provided as part of the assignment |

**Columns:** `employee_id`, `name`, `age`, `salary`, `join_date`, `department`, `gender`, `country`, `city`, `weight_kg`, `is_active`, `review`, `price`, `weight_kg_duplicate`, `target`

## Problems Addressed (15 Tasks)

| # | Problem | Description |
|---|---------|-------------|
| 01 | **Missing Values** | ~8,400 NaN/empty cells across age, salary, join_date, department, gender, country, city, weight_kg, is_active, review, and price filled with median, mode, or forward fill depending on column type. |
| 02 | **Duplicate Rows** | ~300 exact duplicate rows inflating counts and biasing analysis removed using `drop_duplicates()`. |
| 03 | **Duplicate IDs** | ~499 duplicate `employee_id` values violating uniqueness kept first occurrence of each. |
| 04 | **Wrong Date Formats** | `join_date` mixed datetime objects with DD/MM/YYYY strings — standardized to `datetime64` with `pd.to_datetime()`. |
| 05 | **Numeric as String** | `weight_kg` contained values like `"71kg"` stripped the suffix and converted to `float64`. |
| 06 | **Inconsistent Labels** | Country (13 variants → 3), gender (10 variants → 2), and department (mixed casing) standardized with mapping dictionaries. |
| 07 | **Spelling Mistakes** | City typos (Dhka, Chitagong, Slyhet, etc.) and department typos (Mrketing, Finace) corrected with replacement dictionaries. |
| 08 | **Outliers** | Salary values up to 9,999,999 and down to −500 capped using the IQR method (Winsorization). |
| 09 | **Invalid Values** | Ages of −5, 0, 200, 999 and negative prices replaced with NaN, then filled with median. |
| 10 | **Noisy Text** | Meaningless reviews like "ok", "bad", "na", "...", "fine" replaced with "No Review". |
| 11 | **Boolean as String** | `is_active` stored as float (0.0/1.0) converted to proper `bool` type. |
| 12 | **Data Type Issues** | Multiple columns had incorrect dtypes cast all to correct types (int, float, datetime, bool). |
| 13 | **Range Violations** | Enforced business rules: age 18–65, salary 15K–500K, price > 0 — applied `clip()`. |
| 14 | **Class Imbalance** | `target` column 95/5 split balanced with `RandomOverSampler` from imbalanced-learn. |
| 15 | **Schema Validation** | `weight_kg_duplicate` column was 100% null dropped it and validated final 14-column schema. |

## Before vs After Summary

| Metric | Before | After |
|--------|--------|-------|
| Rows | 20,300 | ~19,800 |
| Columns | 15 | 14 |
| Missing values | ~8,400 | 0 |
| Duplicate rows | 300 | 0 |
| Duplicate IDs | 499 | 0 |
| Country variants | 13 | 3 |
| Gender variants | 10 | 2 |
| City typos | 7 | 0 |
| Salary outliers | 500+ | 0 |
| Invalid ages | 300+ | 0 |
| Negative prices | 200+ | 0 |
| Target imbalance | 95%/5% | 50%/50% |

## How to Run

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Ridzzz0Alam/data_cleaning_and_preprocessing.git
   cd data-cleaning-assignment
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Open the notebook:**
   ```bash
   jupyter notebook data_cleaning.ipynb
   ```

4. **Run all cells** (Cell → Run All) - the notebook will load `dirty_dataset.xlsx`, execute all 15 cleaning tasks, and save the result as `cleaned_dataset.csv`.

## Project Structure

```
├── data_cleaning.ipynb        # Main notebook with all 15 tasks
├── dirty_dataset.xlsx         # Original dirty dataset
├── cleaned_dataset.csv        # Output after cleaning (generated)
├── requirements.txt           # Python dependencies
└── README.md                  # This file
```

## Tools & Libraries

- Python 3.x
- pandas
- numpy
- matplotlib
- seaborn
- imbalanced-learn (for RandomOverSampler)
- openpyxl (for reading .xlsx files)
