# SQL Fundamentals

## SELECT - Reading Data

```sql
-- Select all columns
SELECT * FROM users;

-- Select specific columns
SELECT name, email FROM users;

-- With alias
SELECT name AS user_name, email AS user_email FROM users;

-- Distinct values
SELECT DISTINCT country FROM users;

-- Limit results
SELECT * FROM users LIMIT 10;
SELECT * FROM users LIMIT 10 OFFSET 20;  -- Skip first 20
```

---

## WHERE - Filtering

```sql
-- Basic conditions
SELECT * FROM users WHERE age >= 18;
SELECT * FROM users WHERE status = 'active';

-- Multiple conditions
SELECT * FROM users WHERE age >= 18 AND status = 'active';
SELECT * FROM users WHERE country = 'USA' OR country = 'UK';

-- IN / NOT IN
SELECT * FROM users WHERE country IN ('USA', 'UK', 'Canada');

-- BETWEEN
SELECT * FROM users WHERE age BETWEEN 18 AND 30;

-- LIKE (pattern matching)
SELECT * FROM users WHERE name LIKE 'J%';      -- Starts with J
SELECT * FROM users WHERE email LIKE '%@gmail.com';

-- NULL checks
SELECT * FROM users WHERE phone IS NULL;
SELECT * FROM users WHERE phone IS NOT NULL;
```

---

## ORDER BY - Sorting

```sql
-- Ascending (default)
SELECT * FROM users ORDER BY name;
SELECT * FROM users ORDER BY name ASC;

-- Descending
SELECT * FROM users ORDER BY created_at DESC;

-- Multiple columns
SELECT * FROM users ORDER BY country, name;
```

---

## INSERT - Adding Data

```sql
-- Insert single row
INSERT INTO users (name, email, age)
VALUES ('John', 'john@example.com', 30);

-- Insert multiple rows
INSERT INTO users (name, email, age)
VALUES 
    ('John', 'john@example.com', 30),
    ('Jane', 'jane@example.com', 25),
    ('Bob', 'bob@example.com', 35);
```

---

## UPDATE - Modifying Data

```sql
-- Update specific rows
UPDATE users SET status = 'inactive' WHERE id = 1;

-- Update multiple columns
UPDATE users 
SET name = 'John Doe', email = 'johndoe@example.com'
WHERE id = 1;

-- Update with calculation
UPDATE products SET price = price * 1.1;  -- 10% increase
```

---

## DELETE - Removing Data

```sql
-- Delete specific rows
DELETE FROM users WHERE id = 1;

-- Delete with condition
DELETE FROM users WHERE status = 'inactive';

-- Delete all rows (careful!)
DELETE FROM users;

-- Truncate (faster, resets auto-increment)
TRUNCATE TABLE users;
```

---

## Aggregate Functions

```sql
-- Count
SELECT COUNT(*) FROM users;
SELECT COUNT(DISTINCT country) FROM users;

-- Sum, Average, Min, Max
SELECT SUM(amount) FROM orders;
SELECT AVG(price) FROM products;
SELECT MIN(age), MAX(age) FROM users;

-- With GROUP BY
SELECT country, COUNT(*) as user_count
FROM users
GROUP BY country;

-- With HAVING (filter groups)
SELECT country, COUNT(*) as user_count
FROM users
GROUP BY country
HAVING COUNT(*) > 10;
```

---

## JOINS

> JOINs combine data from multiple tables based on related columns

```sql
-- INNER JOIN - only returns rows that have matches in BOTH tables
SELECT users.name, orders.total
FROM users
INNER JOIN orders ON users.id = orders.user_id;

-- LEFT JOIN - all users, even if they have no orders (orders = NULL)
SELECT users.name, orders.total
FROM users
LEFT JOIN orders ON users.id = orders.user_id;

-- RIGHT JOIN - all orders, even if user is missing (rarely used)
SELECT users.name, orders.total
FROM users
RIGHT JOIN orders ON users.id = orders.user_id;

-- Multiple joins
SELECT u.name, o.total, p.name as product
FROM users u
JOIN orders o ON u.id = o.user_id
JOIN products p ON o.product_id = p.id;
```

---

## Subqueries

```sql
-- In WHERE clause
SELECT * FROM users
WHERE id IN (SELECT user_id FROM orders WHERE total > 100);

-- In SELECT clause
SELECT name,
    (SELECT COUNT(*) FROM orders WHERE orders.user_id = users.id) as order_count
FROM users;

-- In FROM clause
SELECT avg_total FROM (
    SELECT AVG(total) as avg_total FROM orders GROUP BY user_id
) as subquery;
```

---

## CREATE TABLE

```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    age INT,
    status VARCHAR(20) DEFAULT 'active',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- With foreign key
CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    total DECIMAL(10, 2),
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

---

## ALTER TABLE

```sql
-- Add column
ALTER TABLE users ADD COLUMN phone VARCHAR(20);

-- Modify column
ALTER TABLE users MODIFY COLUMN phone VARCHAR(30);

-- Drop column
ALTER TABLE users DROP COLUMN phone;

-- Add index
ALTER TABLE users ADD INDEX idx_email (email);

-- Add foreign key
ALTER TABLE orders ADD FOREIGN KEY (user_id) REFERENCES users(id);
```

---

## Common Data Types

```sql
-- Numeric
INT                     -- Integer
BIGINT                  -- Large integer
DECIMAL(10, 2)          -- Exact decimal (10 digits, 2 after point)
FLOAT, DOUBLE           -- Floating point

-- String
CHAR(10)                -- Fixed length
VARCHAR(255)            -- Variable length
TEXT                    -- Long text

-- Date/Time
DATE                    -- Date only
TIME                    -- Time only
DATETIME                -- Date and time
TIMESTAMP               -- Unix timestamp

-- Boolean
BOOLEAN                 -- TRUE/FALSE
```

---

## Indexes

```sql
-- Create index
CREATE INDEX idx_email ON users(email);

-- Unique index
CREATE UNIQUE INDEX idx_email ON users(email);

-- Composite index
CREATE INDEX idx_name_email ON users(name, email);

-- Drop index
DROP INDEX idx_email ON users;
```

---

## Views

```sql
-- Create view
CREATE VIEW active_users AS
SELECT id, name, email
FROM users
WHERE status = 'active';

-- Use view
SELECT * FROM active_users;

-- Drop view
DROP VIEW active_users;
```

---

## Useful Functions

```sql
-- String functions
CONCAT(first_name, ' ', last_name)
UPPER(name), LOWER(name)
LENGTH(name)
SUBSTRING(name, 1, 3)
TRIM(name)

-- Date functions
NOW()                   -- Current datetime
CURDATE()               -- Current date
DATE_FORMAT(date, '%Y-%m-%d')
DATEDIFF(date1, date2)
DATE_ADD(date, INTERVAL 1 DAY)

-- Conditional
COALESCE(phone, 'N/A')  -- First non-null
IF(age >= 18, 'Adult', 'Minor')
CASE 
    WHEN age >= 18 THEN 'Adult'
    WHEN age >= 13 THEN 'Teen'
    ELSE 'Child'
END
```

---

## Transactions

```sql
-- Start transaction
START TRANSACTION;

-- Operations
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;

-- Commit changes
COMMIT;

-- Or rollback on error
ROLLBACK;
```