# Advanced SQL Concepts Assignment 🚀
**Course:** Database Programming

---

## 👤 Academic Information
* **Student ID:** 31491

---

## 📌 Project Overview
This repository contains the practical implementation of Advanced SQL concepts including **Common Table Expressions (CTEs)** and **Window Functions** using Oracle Database (SQL*Plus).

---

## 📁 Part A: Common Table Expressions (CTEs)
1_sales_table_data.jpg
### 1. Database Setup & Initial Data
* **SQL Query:** 
```sql
SELECT * FROM Sales;




2. Simple CTE
​SQL Query:
    WITH ElectronicsProducts AS (
    SELECT ProductID, ProductName, Price 
    FROM Products 
    WHERE Category = 'Electronics'
)
SELECT * FROM ElectronicsProducts;

2_simple_cte.jpg


3. Multiple CTEs
​SQL Query:
    WITH KigaliCustomers AS (
    SELECT CustomerID FROM Customers WHERE Region = 'Kigali'
),
HighValueSales AS (
    SELECT SaleID, CustomerID, TotalAmount FROM Sales WHERE TotalAmount >= 1000
)
SELECT h.SaleID, h.TotalAmount 
FROM HighValueSales h
JOIN KigaliCustomers k ON h.CustomerID = k.CustomerID;

Output(image 3):


4. Recursive CTE
​SQL Query
    WITH MonthsOfYear (MonthNumber) AS (
    SELECT 1 FROM DUAL
    UNION ALL
    SELECT MonthNumber + 1 FROM MonthsOfYear WHERE MonthNumber < 12
)
SELECT MonthNumber FROM MonthsOfYear;

Output(image 4):


5. CTE with Aggregation
​SQL Query:

    WITH CustomerSpending AS (
    SELECT CustomerID, SUM(TotalAmount) AS TotalSpent
    FROM Sales
    GROUP BY CustomerID
)
SELECT c.CustomerName, s.TotalSpent 
FROM Customers c
JOIN CustomerSpending s ON c.CustomerID = s.CustomerID;

Output(image 5):


6. CTE Combined with JOIN
​SQL Query:
    WITH DetailedSales AS (
    SELECT SaleID, CustomerID, ProductID, TotalAmount FROM Sales
)
SELECT ds.SaleID, c.CustomerName, p.ProductName, ds.TotalAmount
FROM DetailedSales ds
JOIN Customers c ON ds.CustomerID = c.CustomerID
JOIN Products p ON ds.ProductID = p.ProductID;

Output(image 6):


📁 Part B: Window Functions
​7. Ranking Functions
​SQL Query:
    SELECT SaleID, TotalAmount,
ROW_NUMBER() OVER (ORDER BY TotalAmount DESC) AS RowNum,
RANK() OVER (ORDER BY TotalAmount DESC) AS SalesRank,
DENSE_RANK() OVER (ORDER BY TotalAmount DESC) AS DenseRank,
PERCENT_RANK() OVER (ORDER BY TotalAmount DESC) AS PercentRank
FROM Sales;

Output(image 7):


8. Aggregate Window Functions
​SQL Query:
    SELECT SaleID, CustomerID, TotalAmount, 
SUM(TotalAmount) OVER (PARTITION BY CustomerID) AS Total, 
AVG(TotalAmount) OVER (PARTITION BY CustomerID) AS AvgAmt, 
MIN(TotalAmount) OVER (PARTITION BY CustomerID) AS MinAmt, 
MAX(TotalAmount) OVER (PARTITION BY CustomerID) AS MaxAmt 
FROM Sales;

Output(image 8):


9. Navigation Functions
​SQL Query:
    SELECT SaleID, SaleDate, TotalAmount, 
LAG(TotalAmount, 1) OVER (ORDER BY SaleDate) AS Prev, 
LEAD(TotalAmount, 1) OVER (ORDER BY SaleDate) AS Next 
FROM Sales;

Output(image 9):

10. Distribution Functions
​SQL Query:
    SELECT SaleID, TotalAmount, 
NTILE(3) OVER (ORDER BY TotalAmount DESC) AS Tier, 
CUME_DIST() OVER (ORDER BY TotalAmount DESC) AS Dist 
FROM Sales;
    
Output(image 10):






















