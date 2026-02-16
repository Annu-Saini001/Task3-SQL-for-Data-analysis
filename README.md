# Task3-SQL-for-Data-analysis
using uk_ecommerce for sql for data analysis

CREATE DATABASE ecommerce;
USE ecommerce;


CREATE TABLE transactions (
    InvoiceNo VARCHAR(20),
    StockCode VARCHAR(20),
    Description TEXT,
    Quantity INT,
    InvoiceDate VARCHAR(50),   -- TEMPORARY as string
    UnitPrice DECIMAL(10,2),
    CustomerID VARCHAR(20),
    Country VARCHAR(50)
);


LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/data.csv'
INTO TABLE transactions
CHARACTER SET latin1
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n'
IGNORE 1 ROWS
(@InvoiceNo, @StockCode, @Description, @Quantity, @InvoiceDate, @UnitPrice, @CustomerID, @Country)
SET
InvoiceNo = @InvoiceNo,
StockCode = @StockCode,
Description = @Description,
Quantity = @Quantity,
InvoiceDate = STR_TO_DATE(@InvoiceDate, '%m/%d/%Y %H:%i'),
UnitPrice = @UnitPrice,
CustomerID = NULLIF(@CustomerID,''),
Country = @Country;
SET SQL_SAFE_UPDATES = 0;

DELETE FROM transactions
WHERE UnitPrice <= 0 OR UnitPrice IS NULL;

-- See first 10 rows
SELECT * FROM transactions LIMIT 10;

-- Check column types and count
DESCRIBE transactions;

-- Check number of rows
SELECT COUNT(*) FROM transactions;

-- Select all transactions
SELECT * FROM transactions LIMIT 20;

-- Select specific columns
SELECT InvoiceNo, CustomerID, UnitPrice, Quantity FROM transactions LIMIT 20;
 
 
 -- Transactions from the UK only
SELECT * FROM transactions
WHERE Country = 'United Kingdom';

-- Transactions with price > 100
SELECT * FROM transactions
WHERE UnitPrice > 100;
   
   
-- Highest priced transactions
SELECT * FROM transactions
ORDER BY UnitPrice DESC
LIMIT 20;

-- Earliest transactions first
SELECT * FROM transactions
ORDER BY InvoiceDate ASC
LIMIT 20;
   

-- Total revenue
SELECT SUM(UnitPrice * Quantity) AS TotalRevenue FROM transactions;

-- Average transaction value
SELECT AVG(UnitPrice * Quantity) AS AvgOrderValue FROM transactions;

-- Revenue by country
SELECT Country, SUM(UnitPrice * Quantity) AS Revenue
FROM transactions
GROUP BY Country
ORDER BY Revenue DESC;

![image alt](https://raw.githubusercontent.com/Annu-Saini001/Task3-SQL-for-Data-analysis/6490dc700f03a75ca07f01b10fadee916f727965/uk_ecommerce_sql_analysis/Screenshot%202026-02-16%20200846.png)
![image alt](https://raw.githubusercontent.com/Annu-Saini001/Task3-SQL-for-Data-analysis/6490dc700f03a75ca07f01b10fadee916f727965/uk_ecommerce_sql_analysis/Screenshot%202026-02-16%20202406.png)
![image alt](https://raw.githubusercontent.com/Annu-Saini001/Task3-SQL-for-Data-analysis/6490dc700f03a75ca07f01b10fadee916f727965/uk_ecommerce_sql_analysis/Screenshot%202026-02-16%20202422.png)
![image alt](https://raw.githubusercontent.com/Annu-Saini001/Task3-SQL-for-Data-analysis/6490dc700f03a75ca07f01b10fadee916f727965/uk_ecommerce_sql_analysis/Screenshot%202026-02-16%20202725.png)
![image alt](https://raw.githubusercontent.com/Annu-Saini001/Task3-SQL-for-Data-analysis/6490dc700f03a75ca07f01b10fadee916f727965/uk_ecommerce_sql_analysis/Screenshot%202026-02-16%20203014.png)
![image alt](https://raw.githubusercontent.com/Annu-Saini001/Task3-SQL-for-Data-analysis/6490dc700f03a75ca07f01b10fadee916f727965/uk_ecommerce_sql_analysis/Screenshot%202026-02-16%20203108.png)
![image alt](https://raw.githubusercontent.com/Annu-Saini001/Task3-SQL-for-Data-analysis/6490dc700f03a75ca07f01b10fadee916f727965/uk_ecommerce_sql_analysis/Screenshot%202026-02-16%20203255.png)
![image alt](https://raw.githubusercontent.com/Annu-Saini001/Task3-SQL-for-Data-analysis/6490dc700f03a75ca07f01b10fadee916f727965/uk_ecommerce_sql_analysis/Screenshot%202026-02-16%20203444.png)
