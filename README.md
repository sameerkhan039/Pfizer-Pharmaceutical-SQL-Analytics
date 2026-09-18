# Pfizer Pharmaceutical Inventory & Pricing Analytics 💊📊

An end-to-end data analytics project analyzing pharmaceutical inventory, pricing tiers, and stock availability using advanced SQL for data extraction/transformation and Microsoft Power BI for interactive visualization.

---

## 🚀 Project Overview
This project evaluates pharmaceutical retail performance, focusing on pricing distribution, pre/post-discount trends, stock availability status, and top company metrics. The entire data processing workflow is driven by optimized SQL queries, ensuring a lightweight and high-performing Power BI dashboard model.

---

## 🛠️ Technical Workflow & Tools
1. **Data Extraction & Transformation (SQL):** 
   - Handled data cleaning, aggregation, and ranking.
   - Utilized window functions, Common Table Expressions (CTEs), and conditional `CASE` statements to categorize pricing tiers.
2. **Data Visualization (Power BI):** 
   - Built a custom, modern dashboard featuring KPI summary cards, trend analysis lines, dynamic slicers, and categorical breakdowns.

---

## 📝 Key SQL Insights & Queries
```sql
1. Top Companies by Pharmaceutical Count & Average Pre-Discount
SELECT 
    Company,
    COUNT(DISTINCT Name) AS No_Of_Pharma,
    ROUND(AVG(Price_before), 0) AS Average_pre_discont
FROM pakistan
GROUP BY Company
ORDER BY 2 DESC;

2. Out-of-Stock Analysis by Company
SELECT 
    Availability,
    Company,
    COUNT(Availability) AS No_Of_Out_Of_Sold
FROM pakistan
WHERE Availability = 'Sold Out'
GROUP BY 2
ORDER BY 3 DESC;

3. Price Drop Comparison
select Name , 
Price_before , 
Price_after , 
(Price_before - Price_after) as Price_Drop,  
rank() over(order by Price_Drop desc) as ranks 
from pakistan
limit 5;

4. Pricing Tier Categorization
SELECT 
    Name,
    Price_After AS Total_Price,
    CASE
        WHEN Price_After >= 1000 THEN 'High Price'
        WHEN Price_After >= 500 THEN 'Medium Price'
        ELSE 'Low Price'
    END AS Range_Categorization
FROM

5. Company-wise machine status details
SELECT 
    Company, Availability, COUNT(*) AS Total_Availability
FROM
    pakistan
GROUP BY 1 , 2
ORDER BY 2 ASC , 3 DESC
    pakistan
