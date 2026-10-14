# Customer Shopping Behavior Analysis

An end-to-end data analytics project exploring **3,900 customer purchases** to understand shopping patterns, customer segments, product preferences, discount usage, shipping choices, and subscription behavior.

The project combines **Python (Pandas)** for data cleaning and feature engineering, **PostgreSQL** for business-focused SQL analysis, and **Power BI** for an interactive dashboard.

## Project Overview

The goal is to turn transaction-level shopping data into insights that can support marketing, customer retention, and product decisions.

### Project highlights

- Cleaned and prepared customer shopping data with Python and Pandas.
- Handled missing values in `Review Rating` using the median rating within each product category.
- Standardized column names to `snake_case`.
- Created an `age_group` feature and converted purchase frequency into an approximate number of days.
- Loaded the prepared data into PostgreSQL for SQL analysis.
- Wrote SQL queries to answer 10 business questions.
- Created a Power BI dashboard to communicate findings visually.

## Tools & Technologies

- **Python** — data preparation and feature engineering
- **Pandas** — data manipulation and analysis
- **Jupyter Notebook** — exploratory analysis workflow
- **PostgreSQL** — database and SQL analysis
- **SQLAlchemy** and **psycopg2-binary** — Python-to-PostgreSQL connection
- **Power BI** — interactive dashboard
- **Microsoft PowerPoint / PDF** — project presentation and report

## Dataset

The analysis report describes a dataset containing:

- **3,900 rows / purchases**
- **18 original columns**
- **37 missing values** in the `Review Rating` column

The fields cover customer demographics, purchase details, shopping behavior, discounts, shipping type, subscription status, and review ratings.

> The original CSV dataset was not included among the uploaded project files. Add the dataset locally before running the notebook. Do not commit private, licensed, or sensitive customer data to a public repository.

## Repository Structure

A suggested GitHub structure for the files in this project:

```text
customer-shopping-behavior-analysis/
├── README.md
├── customer behavior.ipynb
├── customer_shopping.sql
├── Customer behavior dashboard.pbix
├── Customer-Shopping-Behavior-Analysis.pptx
├── Customer Shopping Behavior Analysis.pdf
└── data/
    └── customer_shopping_behavior.csv   # add locally; commit only if permitted
```

Keep filenames consistent with the actual files in your repository. You can rename files to remove spaces if you prefer, but update any file paths accordingly.

## Data Preparation Workflow

The notebook performs these main steps:

1. Imports the dataset using Pandas.
2. Inspects the dataset structure and summary statistics.
3. Checks missing values.
4. Fills missing review ratings using the median rating for the corresponding category.
5. Converts column names to lowercase and replaces spaces with underscores.
6. Renames `purchase_amount_(usd)` to `purchase_amount`.
7. Creates `age_group` using age quartiles and labels: `Young Adult`, `Adult`, `Middle-aged`, and `Senior`.
8. Maps purchase-frequency categories to approximate day counts in `purchase_frequency_days`.
9. Checks the relationship between `discount_applied` and `promo_code_used`, then drops `promo_code_used`.
10. Loads the cleaned DataFrame into a PostgreSQL table named `customer`.

## SQL Business Questions

The SQL script (`customer_shopping.sql`) contains queries exploring:

1. Total revenue by gender.
2. Customers who used a discount but spent at least the average purchase amount.
3. Five products with the highest average review ratings.
4. Average purchase amount for Standard versus Express shipping.
5. Customer count, average spend, and total revenue by subscription status.
6. Five products with the highest percentage of purchases using discounts.
7. Customer segmentation into New, Returning, and Loyal groups based on previous purchases.
8. The three most-purchased products within each category.
9. Subscription status among customers with more than five previous purchases.
10. Revenue contribution by age group.

The SQL file uses PostgreSQL-compatible syntax, including `::numeric` casts and window functions.

## Key Findings Reported

The accompanying report/presentation highlights the following findings:

- Female customers generated slightly higher total revenue than male customers.
- Express-shipping customers had an average purchase amount of about **$65**, compared with about **$58** for Standard shipping; the report describes Express customers as spending approximately 12% more per transaction.
- The report states that subscribers spend more than non-subscribers and contribute a substantial share of revenue.
- The report presents customer segments as approximately **50% New**, **35% Returning**, and **15% Loyal**.
- Blouse, Dress, and Shirt are highlighted among the top-rated products.
- Suggested actions include strengthening subscription benefits, rewarding repeat customers, reviewing discount strategy, promoting highly rated products, and targeting high-revenue customer groups.

These are findings reported in the supplied project materials; rerun the notebook, SQL queries, and dashboard to reproduce or validate the figures against your dataset.

## Setup and Usage

### 1. Clone or download the repository

```bash
git clone <your-repository-url>
cd customer-shopping-behavior-analysis
```

Replace `<your-repository-url>` with your GitHub repository URL.

### 2. Create a Python environment (recommended)

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Install the Python dependencies:

```bash
pip install pandas jupyter sqlalchemy psycopg2-binary
```

### 3. Add the CSV dataset

Place the permitted dataset file at:

```text
customer_shopping_behavior.csv
```

In `customer behavior.ipynb`, update the `pd.read_csv(...)` path to match where you saved the CSV. The uploaded notebook currently uses a machine-specific Windows path, so that path will not work on other computers without modification.

### 4. Set up PostgreSQL

1. Install and start PostgreSQL.
2. Create a database named `customer_behavior`.
3. Ensure the PostgreSQL service is running and note your local connection details.
4. Configure credentials securely before running the notebook's database-loading cell.

**Security note:** Do not put your real database password directly in a notebook or commit it to GitHub. Use environment variables or a local, untracked `.env` file instead. If a real password was included in any uploaded or previously committed file, change/rotate it before publishing the repository.

For example, set environment variables in PowerShell for the current terminal session:

```powershell
$env:PGHOST = "localhost"
$env:PGPORT = "5432"
$env:PGDATABASE = "customer_behavior"
$env:PGUSER = "postgres"
$env:PGPASSWORD = "replace-with-your-local-password"
```

Then adapt the notebook's database connection code to read those variables rather than containing a password literal.

### 5. Run the notebook

```bash
jupyter notebook
```

Open `customer behavior.ipynb` and run the cells in order. Confirm the CSV path and PostgreSQL settings first.

### 6. Run the SQL analysis

Open `customer_shopping.sql` in pgAdmin or another PostgreSQL client connected to `customer_behavior`. The notebook is configured to load the cleaned data into a table named `customer`.

### 7. Open the Power BI dashboard

Open `Customer behavior dashboard.pbix` in Power BI Desktop. If prompted, configure the data source and refresh the report as appropriate for your local setup.

## Dashboard & Project Report

The repository includes a Power BI `.pbix` dashboard file, a PowerPoint presentation, and a PDF report. Add screenshots of the dashboard to the repository if you want the README to display a preview. No screenshot is embedded in this README yet.

## Recommendations

The supplied report suggests these potential business actions:

- **Boost subscriptions:** communicate subscriber benefits and encourage sign-ups.
- **Build loyalty:** reward repeat purchases and help returning customers become loyal customers.
- **Review discount policy:** evaluate discount effectiveness while considering profit margins.
- **Improve product positioning:** feature highly rated and best-selling products.
- **Target marketing:** focus on high-revenue age groups and customers with relevant shipping preferences.

## Limitations & Notes

- The raw CSV dataset was not part of the uploaded files, so the setup instructions assume you will provide it separately.
- Database credentials and local file paths must be configured for each machine.
- The reported findings should be validated by running the analysis against the dataset.
- The SQL segmentation classifies `previous_purchases = 1` as `New`, values from 2 to 10 as `Returning`, and other values as `Loyal`, as written in the supplied SQL. Confirm that these thresholds match your intended business definitions.

## Future Improvements

- Add a `requirements.txt` file for reproducible dependency installation.
- Replace machine-specific paths with configurable relative paths.
- Move database credentials into environment variables.
- Add dashboard screenshots or a short GIF.
- Add automated data-quality checks and document metric definitions.
- Add a data dictionary for all columns.

## Author

** ADITYA VISHWAKARMA**

If you find this project useful, feel free to star the repository.
