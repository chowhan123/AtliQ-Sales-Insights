# AtliQ-Sales-Insights
Power BI dashboard project visualizing AtliQ Hardware’s ₹984M+ sales, 2M+ units sold, top-performing cities, and projected 7% revenue growth — built to support data-driven business decisions.

## Sales Insights Data Analysis Project

This project is a comprehensive **Sales Insights Dashboard** developed using **MySQL** for backend data querying and **Power BI** for advanced data visualization. The purpose of this project is to explore, analyze, and visualize transactional sales data across regions, currencies, and time periods. The key goal is to help stakeholders make informed decisions based on revenue performance, customer behavior, and market trends.

---

### Setup Instructions (MySQL on Local Machine)

1. Install MySQL on your system.

2. Download the SQL database file: [Database\_Dataset.sql](.https://github.com/chowhan123/AtliQ-Sales-Insights/blob/main/README.md).
   
3. Import `Database_Dataset.sql` into your MySQL environment using standard MySQL import commands.

---

## Data Analysis Using SQL

### 1. Show all customer records

```sql
SELECT * FROM customers;
```

### 2. Show total number of customers

```sql
SELECT COUNT(*) FROM customers;
```

### 3. Show transactions for Chennai market (Market Code: Mark001)

```sql
SELECT * FROM transactions WHERE market_code = 'Mark001';
```

### 4. Show distinct product codes sold in Chennai

```sql
SELECT DISTINCT product_code FROM transactions WHERE market_code = 'Mark001';
```

### 5. Show transactions where currency is US dollars

```sql
SELECT * FROM transactions WHERE currency = 'USD';
```

### 6. Show transactions from 2020 (joined with date table)

```sql
SELECT transactions.*, date.*
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020;
```

### 7. Show total revenue in 2020

```sql
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020 AND (transactions.currency = 'INR' OR transactions.currency = 'USD');
```

### 8. Show total revenue in January 2020

```sql
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020 AND date.month_name = 'January' AND (transactions.currency = 'INR' OR transactions.currency = 'USD');
```

### 9. Show total revenue in Chennai in 2020

```sql
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020 AND transactions.market_code = 'Mark001';
```

---

## Data Transformation Using Power BI

### Formula to Create `norm_amount` Column

To normalize sales values based on currency:

```powerquery
= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] = "USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)
```

This Power Query formula converts USD to INR using a multiplier (e.g., ₹1 = \$75) for comparative analysis.

---



Feel free to fork this repo, practice SQL queries, and explore interactive dashboards using Power BI!

