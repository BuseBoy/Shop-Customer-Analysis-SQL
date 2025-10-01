-- ========================================
-- Customer Analysis SQL Queries
-- Description: Customer segmentation and spending behavior analysis
-- ========================================

-- 1) Preview the first 100 rows from the customers table
SELECT *
FROM customers
LIMIT 100;
-- Initial data check. We can see the structure of the dataset, types of variables, and possible anomalies. 

-- Customers table columns:
-- customer_id → Unique identifier for each customer
-- gender → Customer gender (e.g., Male/Female)
-- age → Customer age in years
-- annual_income → Annual income of the customer
-- spending_score → Score representing spending behavior (likely 1–100)
-- profession → Customer’s profession/occupation
-- work_experience → Years of work experience
-- family_size → Number of family members

-- 2) Check uniqueness of customer_id
SELECT COUNT(DISTINCT customer_id) AS distinct_data
FROM customers;
-- Each customer_id is unique, meaning there are no duplicate customer records.

-- 3) Check for missing or null values
SELECT *
FROM customers
WHERE customer_id IS NULL
   OR gender IS NULL OR gender = ''
   OR age IS NULL
   OR annual_income IS NULL
   OR spending_score IS NULL
   OR profession IS NULL OR profession = ''
   OR work_experience IS NULL
   OR family_size IS NULL;
-- There are no nulls except for 35 missing profession values.
-- Since other columns are complete, we can fill missing profession values with 'Unknown'.

UPDATE customers
SET profession = 'Unknown'
WHERE profession IS NULL OR profession = '';

-- 4) Create a view for customer segmentation by income and age
CREATE VIEW customer_segments AS
SELECT 
    customer_id,
    annual_income,
    age,
    spending_score,
    profession,
    family_size,
    -- Income segmentation
    CASE
        WHEN annual_income < 30000 THEN 'Low Income'
        WHEN annual_income BETWEEN 30000 AND 60000 THEN 'Middle Income'
        WHEN annual_income BETWEEN 60001 AND 90000 THEN 'High Income'
        ELSE 'Very High Income'
    END AS income_segment,
    -- Age segmentation
    CASE
        WHEN age < 25 THEN 'Gen Z (18-24)'
        WHEN age BETWEEN 25 AND 35 THEN 'Millennial (25-35)'  
        WHEN age BETWEEN 36 AND 50 THEN 'Gen X (36-50)'
        WHEN age BETWEEN 51 AND 65 THEN 'Boomer (51-65)'
        ELSE 'Senior (65+)'
    END AS age_group
FROM customers;
-- Segments allow analyzing spending patterns and targeting marketing campaigns.

-- 5) Analyze average spending by income + age combination
SELECT 
    income_segment,
    age_group,
    AVG(spending_score) AS avg_spending_score,
    COUNT(*) AS num_customers
FROM customer_segments
GROUP BY income_segment, age_group
ORDER BY avg_spending_score DESC;
-- Young Low Income (18–35): High spending potential, yet the number of customers in this group is low → consider offering referral programs such as "Bring a Friend, Get a Bonus" to attract more customers. Analyzing which products they buy most is a good way to promote those products on social media platforms, where young people are the primary users.
-- High/Very High Income: Large customer base but moderate average spending → consider offering higher discounts or bonuses to encourage increased spending.
-- Middle- and Low-Income Gen X & Boomers: Lower spending → appeal to them with value-for-money products, savings-focused deals, or family packages.

-- 6) Top spenders by income segment
SELECT 
    income_segment, 
    AVG(spending_score) AS avg_spending_score,
    COUNT(*) AS num_customers
FROM customer_segments
GROUP BY income_segment
ORDER BY avg_spending_score DESC;
-- Very-high-income group has the highest spending score with the highest customer number. 
-- Yet, other groups have close spending scores with each other.
-- By also considering the income + age segments, both the segment sizes and their average spending scores are reasonable, so there is little expectation of outliers.

-- 7) Top spenders by age group
SELECT 
    age_group,
    AVG(spending_score) AS avg_spending_score,
    COUNT(*) AS num_customers
FROM customer_segments
GROUP BY age_group
ORDER BY avg_spending_score DESC;
-- Spending slightly decreases with age; no significant outlier risk in these age segments.

-- 8) Average spending by profession
SELECT 
    profession, 
    AVG(spending_score) AS avg_spending,
    COUNT(profession) AS num_profession
FROM customers
GROUP BY profession
ORDER BY avg_spending DESC;
-- Profession has some variation in average spending, but overall it doesn’t strongly influence spending behavior.

-- 9) Average spending by family size
SELECT 
    family_size, 
    AVG(spending_score) AS avg_spending,
    COUNT(family_size) AS num_family_size
FROM customers
GROUP BY family_size
ORDER BY avg_spending DESC;
-- Spending behavior does not significantly change with family
