# Shop Customer Analysis with SQL

This project analyzes customer data from an imaginary retail shop to understand how demographics and background factors influence spending behavior by using PostgreSQL. The goal is to create meaningful customer segments and provide insights that could be applied to marketing strategies, loyalty programs, and product targeting.

Dataset source: [Kaggle - Customers Dataset](https://www.kaggle.com/datasets/datascientistanna/customers-dataset)

## SQL Techniques Used:
- Data Quality Checks: COUNT(DISTINCT), IS NULL, conditional filtering
- Data Manipulation: UPDATE statements for data cleaning
- Database Views: CREATE VIEW for reusable segmentation logic
- Conditional Logic: CASE WHEN statements for multi-level categorization
- Aggregate Functions: AVG(), COUNT() for statistical analysis
- Grouping & Sorting: GROUP BY, ORDER BY for segment-level insights
- Filtering: WHERE clauses for targeted data extraction
 -Aliasing: Column and table aliases for readable queries

## Files
- `dump-postgres-202510012109.sql` → PostgreSQL dump file (backup of the database).
- `shop-customer-analysis.sql` → SQL queries used for analysis.
- `README.md` → Project documentation.

## How to Restore the Database
pg_restore --verbose --host=localhost --port=5432 --username=postgres --dbname=postgres dump-postgres-202510012109.sql


## 📊 Dataset Information
The dataset contains information about customers including demographics, income, and spending behavior.
## Customers Table 

| Column Name     | Data Type    |
|-----------------|--------------|
| customer_id     | int4         |
| annual_income   | int4         |
| age             | int4         |
| spending_score  | int4         |
| profession      | varchar(50)  |
| family_size     | int4         |
| gender          | varchar(10)  |

---
## 🗂️ SQL Analysis Steps

### 1. Preview Data
- Check first 100 rows to understand dataset structure.

### 2. Check Data Quality
- Verified unique `customer_id`.
- Found 35 missing `profession` values → replaced with `'Unknown'`.

### 3. Customer Segmentation
Created a reusable view (`customer_segments`) with:

**Income Segments:**
- Low Income: < $30,000
- Middle Income: $30,000 - $60,000
- High Income: $60,001 - $90,000
- Very High Income: > $90,000

**Age Groups:**
- Gen Z: 18-24 years
- Millennial: 25-35 years
- Gen X: 36-50 years
- Boomer: 51-65 years
- Senior: 65+ years

### 4. Multi-Dimensional Analysis
- Cross-segmentation: Income × Age
- Top spenders identification
- Profession-based spending patterns
- Family size impact analysis
- Gender distribution analysis

---

## 🛠️ Technologies Used
- SQL (PostgreSQL)
- Dataset: Kaggle Customers Dataset  

---

## 📌 How to Use
1. Clone this repository.  
2. Import the dataset into your SQL environment.  
3. Run the queries in `shop-customer-analysis.sql`.  
4. Explore insights and adapt queries for your own segmentation tasks.  
