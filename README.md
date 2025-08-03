# 🎧 SQL Practice – (Chinook Database)

## 📌 Overview
This project documents my  progress in the SQL learning journey using the **Chinook SQLite database**.  
Today’s focus was on **advanced reporting** and **data pivoting techniques** to simulate real-world analytics.

---

## 🗂️ Database Used
- **Chinook SQLite** (download from [Chinook Database GitHub](https://github.com/lerocha/chinook-database))

---

## ✅ Concepts Practiced on Day 7
- 🔹 **Pivoting with CASE + SUM** → creating pivot-style reports  
- 🔹 **Advanced Aggregations** → grouping across multiple dimensions   
- 🔹 **Window Functions** → ranking within aggregated data  
- 🔹 **Percentage Calculations** → finding revenue contribution by category  

---

## 🧠 Business Questions Answered
1. **Total revenue per country per year (pivot report).**  
2. **Top 5 employees (support reps) by total sales.**  
3. **Revenue per genre broken down by media type.**  
4. **Percentage contribution of each genre to overall sales.**  


---

## 💻 Sample Query (Pivot Report: Revenue by Country and Year)
```sql
-- 1. Create a sales report showing total revenue per country per year
SELECT 
    c.Country as Country,
    SUM(CASE WHEN strftime("%Y", i.InvoiceDate)  = "2009" THEN round(i.Total, 2) ELSE 0 END) as Revenue_2009,
    SUM(CASE WHEN strftime("%Y", i.InvoiceDate)  = "2010" THEN i.Total ELSE 0 END) as Revenue_2010,
    SUM(CASE WHEN strftime("%Y", i.InvoiceDate) = "2011" THEN i.Total ELSE 0 END) as Revenue_2011
FROM 
    customers c
JOIN
    invoices i
ON
    c.CustomerId = i.CustomerId	

GROUP BY c.Country

LIMIT 5
