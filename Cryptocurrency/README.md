# 💹 Cryptocurrency SQL Case Study (MySQL Version)

###  Overview
This repository contains SQL analysis queries for a **Cryptocurrency trading case study**, inspired by the *Data With Danny SQL Simplified Labs*.  
The project demonstrates real-world SQL concepts using **MySQL 8.0**, including filtering, aggregation, window functions, and joins.

---

###  Database Setup

**Database:** `cryptocurrency`

**Tables:**
| Table | Description |
|--------|--------------|
| `members` | Contains mentor names and regions. |
| `prices` | Contains historical crypto price and volume data. |
| `transactions` | Records cryptocurrency transactions by members. |

---

###  Files Included
| File | Description |
|------|--------------|
| `cryptocurrency.sql` | All SQL logic for table creation and lab queries. |
| `members.csv` | Mentor information. |
| `prices.csv` | Price and volume history for BTC & ETH. |
| `transactions.csv` | Trading activity dataset. |
| `README.md` | Project overview and usage instructions. |

---

###  SQL Concepts Demonstrated
| Lab | Topic | SQL Features |
|-----|--------|--------------|
| Lab 1 | Basic Queries | `SELECT`, `WHERE`, `ORDER BY`, `LIMIT`, `DISTINCT` |
| Lab 2 | Aggregation | `GROUP BY`, `COUNT`, `MIN`, `MAX`, `AVG` |
| Lab 3 | Data Cleaning | `CASE`, `CAST`, data type conversions |
| Lab 4 | Analytical Functions | `LAG`, `RANK`, rolling averages |
| Lab 5 | Table Joins | `INNER JOIN`, `LEFT JOIN`, multi-table CTEs |

---

###  How to Run

1. Open **MySQL Workbench** or any SQL client.  
2. Execute the following command:
   ```sql
   SOURCE cryptocurrency.sql;


### Load the CSV files into your tables:
LOAD DATA INFILE 'path_to/members.csv' INTO TABLE members
FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n' IGNORE 1 ROWS;

LOAD DATA INFILE 'path_to/prices.csv' INTO TABLE prices
FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n' IGNORE 1 ROWS;

LOAD DATA INFILE 'path_to/transactions.csv' INTO TABLE transactions
FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n' IGNORE 1 ROWS;

Run the Lab sections (Lab 1 to Lab 5) in order.


### Example Output
Example Query: Monthly Cumulative Volume

### 📊 Example Output

**Example Query: Monthly Cumulative Volume**

```sql
WITH cte_monthly_volume AS (
  SELECT
    ticker,
    CAST(DATE_FORMAT(market_date, '%Y-%m-01') AS DATE) AS month_start,
    SUM(
      CASE
        WHEN RIGHT(volume, 1) = 'K' THEN CAST(LEFT(volume, LENGTH(volume)-1) AS DECIMAL(15,2)) * 1000
        WHEN RIGHT(volume, 1) = 'M' THEN CAST(LEFT(volume, LENGTH(volume)-1) AS DECIMAL(15,2)) * 1000000
        WHEN volume = '-' THEN 0
        ELSE CAST(volume AS DECIMAL(15,2))
      END
    ) AS monthly_volume
  FROM prices
  WHERE market_date BETWEEN '2020-01-01' AND '2020-12-31'
  GROUP BY ticker, month_start
)
SELECT
  ticker,
  month_start,
  SUM(monthly_volume) OVER (
    PARTITION BY ticker
    ORDER BY month_start
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
  ) AS cumulative_monthly_volume
FROM cte_monthly_volume
ORDER BY ticker, month_start;



### Author

Sayali Takekar
Data Science
Maharashtra, India
Passionate about SQL and analytics


