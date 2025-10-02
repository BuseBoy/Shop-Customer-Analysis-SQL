# Shop Customer Analysis with SQL

This project analyzes customer data using PostgreSQL.  
Dataset source: [Kaggle - Customers Dataset](https://www.kaggle.com/datasets/datascientistanna/customers-dataset)

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
| income_segment  | text         |
| age_group       | text         |

---

## 🗂️ SQL Analysis Steps

1. **Preview Data**  
   - Check first 100 rows to understand dataset structure.  

2. **Check Data Quality**  
   - Verified unique `customer_id`.  
   - Found 35 missing `profession` values → replaced with `'Unknown'`.  

3. **Customer Segmentation**  
   - Created a view `customer_segments` using **income** and **age groups**.  
   - Income segments: Low, Middle, High, Very High.  
   - Age groups: Gen Z, Millennial, Gen X, Boomer, Senior.  

4. **Spending Behavior Analysis**  
   - **Income + Age**:  
     - Young low-income customers show high spending potential despite small size → suitable for referral campaigns.  
     - High/Very High income groups have large size but only moderate spending → can be targeted with loyalty programs or premium offers.  
     - Middle/Low income older groups show low spending → respond better to value-for-money products.  

   - **Income Only**:  
     - Very high-income group has the highest spending score with the largest customer base.  
     - Other groups have relatively close spending levels.  

   - **Age Only**:  
     - Spending decreases slightly with age.  
     - No significant outlier risk in these segments.  

   - **Profession**:  
     - Some variation (e.g., Entertainment & Artist higher than Homemaker & Unknown).  
     - Overall, profession does not strongly influence spending.  

   - **Family Size**:  
     - Spending is not significantly affected by family size.  

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
