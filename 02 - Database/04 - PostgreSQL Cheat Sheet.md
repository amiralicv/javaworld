---
type: reference
series: Database
tags: [database, postgres, cheatsheet]
---

# 🐘 PostgreSQL Cheat Sheet

> [!abstract] 🧭 Navigation
> 🏠 [[02 - Database/00 - Overview|Database]]

Two different things live here. Keep them separate in your head:

- **psql meta-commands** start with a backslash (`\dt`). They are features of the `psql` program only. No semicolon needed.
- **SQL** is the real language (`SELECT ...`). It always ends with a semicolon `;`.

---

## 1. Connecting (in your terminal, not in psql)

```bash
psql                                  # connect as your OS user
sudo -u postgres psql                 # connect as the superuser (Linux)
psql -U ali -d testdb -h localhost -p 5432
psql -d testdb -f script.sql          # run a .sql file
psql -d testdb -c "SELECT now();"     # run one command and exit
```

Command-line helper tools (wrappers around SQL):

```bash
createdb testdb
dropdb testdb
createuser --interactive ali
dropuser ali
pg_dump testdb > backup.sql
psql testdb < backup.sql
```

---

## 2. psql meta-commands (the ones you actually use)

|Command|What it does|
|---|---|
|`\?`|help for psql commands|
|`\h SELECT`|help for SQL syntax|
|`\l`|list databases|
|`\c dbname`|connect to another database|
|`\dt`|list tables|
|`\d tablename`|describe a table (columns, types, indexes)|
|`\d+ tablename`|same, with more detail|
|`\dn`|list schemas|
|`\du`|list roles/users|
|`\di`|list indexes|
|`\df`|list functions|
|`\dv`|list views|
|`\x`|toggle expanded output (great for wide rows)|
|`\timing`|show how long each query takes|
|`\i file.sql`|run a SQL file|
|`\o out.txt`|send output to a file|
|`\e`|open the last query in an editor|
|`\conninfo`|who am I, where am I connected|
|`\q`|quit|

---

## 3. Databases and schemas

```sql
CREATE DATABASE shop;
DROP DATABASE shop;
ALTER DATABASE shop RENAME TO store;

CREATE SCHEMA sales;
DROP SCHEMA sales CASCADE;
SET search_path TO sales, public;
```

---

## 4. Roles and permissions

In Postgres a "user" is just a role that has LOGIN. There is no separate user object.

```sql
CREATE ROLE ali WITH LOGIN PASSWORD 'secret';
CREATE ROLE readonly;                      -- no login: a group
ALTER ROLE ali WITH PASSWORD 'newsecret';
ALTER ROLE ali WITH SUPERUSER;             -- be careful
ALTER ROLE ali WITH CREATEDB CREATEROLE;
DROP ROLE ali;

GRANT readonly TO ali;                     -- put ali in a group

GRANT CONNECT ON DATABASE shop TO ali;
GRANT USAGE ON SCHEMA public TO ali;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO ali;
GRANT SELECT, INSERT, UPDATE, DELETE ON customers TO ali;
REVOKE INSERT ON customers FROM ali;

-- rights for tables created in the future
ALTER DEFAULT PRIVILEGES IN SCHEMA public
  GRANT SELECT ON TABLES TO readonly;
```

---

## 5. Tables (DDL)

```sql
CREATE TABLE customers (
    id          serial PRIMARY KEY,        -- or: GENERATED ALWAYS AS IDENTITY
    name        text NOT NULL,
    email       text UNIQUE,
    age         integer CHECK (age >= 0),
    country     varchar(2) DEFAULT 'TR',
    created_at  timestamptz DEFAULT now()
);

CREATE TABLE orders (
    id          serial PRIMARY KEY,
    customer_id integer REFERENCES customers(id) ON DELETE CASCADE,
    total       numeric(10,2) NOT NULL,
    ordered_at  date DEFAULT CURRENT_DATE
);

ALTER TABLE customers ADD COLUMN phone text;
ALTER TABLE customers DROP COLUMN phone;
ALTER TABLE customers RENAME COLUMN name TO full_name;
ALTER TABLE customers ALTER COLUMN email SET NOT NULL;
ALTER TABLE customers ADD CONSTRAINT email_lower CHECK (email = lower(email));

DROP TABLE customers;
DROP TABLE customers CASCADE;              -- also drops things depending on it
TRUNCATE customers;                        -- delete all rows, fast
```

### Common data types

`integer` `bigint` `serial` `numeric(p,s)` `real` `text` `varchar(n)` `char(n)` `boolean` `date` `time` `timestamp` `timestamptz` `interval` `uuid` `json` `jsonb` `text[]` (array) `inet` `bytea`

Rule of thumb: use `text` not `varchar`, `numeric` for money, `timestamptz` not `timestamp`.

---

## 6. Changing data (DML)

```sql
INSERT INTO customers (name, email) VALUES ('Ali', 'ali@mail.com');

INSERT INTO customers (name, email) VALUES
  ('Ayse', 'ayse@mail.com'),
  ('Can',  'can@mail.com')
RETURNING id;                              -- gives you back the new ids

UPDATE customers SET country = 'DE' WHERE id = 3;
DELETE FROM customers WHERE created_at < '2024-01-01';

-- insert, or update if it already exists ("upsert")
INSERT INTO customers (email, name) VALUES ('ali@mail.com', 'Ali K')
ON CONFLICT (email) DO UPDATE SET name = EXCLUDED.name;
```

---

## 7. Queries (SELECT)

```sql
SELECT * FROM customers;
SELECT name, email FROM customers WHERE country = 'TR';

SELECT * FROM customers
WHERE age BETWEEN 18 AND 30
  AND name ILIKE 'a%'                      -- ILIKE = case-insensitive
  AND country IN ('TR', 'DE')
  AND email IS NOT NULL
ORDER BY created_at DESC
LIMIT 10 OFFSET 20;
```

Written order vs. execution order — this is the thing beginners get wrong:

```
written:   SELECT → FROM → WHERE → GROUP BY → HAVING → ORDER BY → LIMIT
executed:  FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT
```

That is why you cannot use a `SELECT` alias inside `WHERE`, but you can inside `ORDER BY`.

### Grouping

```sql
SELECT country, count(*) AS n, avg(age) AS avg_age
FROM customers
WHERE age IS NOT NULL
GROUP BY country
HAVING count(*) > 5                        -- HAVING filters groups, WHERE filters rows
ORDER BY n DESC;
```

Aggregates: `count()` `sum()` `avg()` `min()` `max()` `string_agg()` `array_agg()`

### Joins

```sql
SELECT c.name, o.total
FROM customers c
JOIN orders o ON o.customer_id = c.id;          -- INNER: only matches

SELECT c.name, o.total
FROM customers c
LEFT JOIN orders o ON o.customer_id = c.id;     -- all customers, NULL if no order

-- also: RIGHT JOIN, FULL JOIN, CROSS JOIN
```

### Useful extras

```sql
SELECT DISTINCT country FROM customers;

SELECT name FROM customers
UNION SELECT name FROM suppliers;               -- UNION ALL keeps duplicates

-- subquery
SELECT * FROM customers
WHERE id IN (SELECT customer_id FROM orders WHERE total > 100);

-- CTE: name a subquery, much easier to read
WITH big_orders AS (
    SELECT customer_id, sum(total) AS spent
    FROM orders GROUP BY customer_id
)
SELECT c.name, b.spent
FROM customers c JOIN big_orders b ON b.customer_id = c.id
WHERE b.spent > 1000;

-- window function: aggregate without collapsing rows
SELECT name, country, total,
       rank() OVER (PARTITION BY country ORDER BY total DESC) AS rk
FROM orders JOIN customers ON customers.id = orders.customer_id;

-- conditional
SELECT name, CASE WHEN age < 18 THEN 'minor' ELSE 'adult' END AS group FROM customers;

COALESCE(phone, 'unknown')                      -- first non-NULL value
NULLIF(a, b)                                    -- NULL if a = b
```

---

## 8. Views and indexes

```sql
CREATE VIEW active_customers AS
  SELECT * FROM customers WHERE created_at > now() - interval '1 year';
DROP VIEW active_customers;

CREATE MATERIALIZED VIEW sales_summary AS SELECT ...;
REFRESH MATERIALIZED VIEW sales_summary;

CREATE INDEX idx_orders_customer ON orders(customer_id);
CREATE UNIQUE INDEX idx_email ON customers(lower(email));
DROP INDEX idx_orders_customer;
```

---

## 9. Transactions

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;                                    -- or ROLLBACK;

SAVEPOINT sp1;
ROLLBACK TO sp1;
```

---

## 10. Inspecting and fixing

```sql
EXPLAIN SELECT ...;                        -- the plan
EXPLAIN ANALYZE SELECT ...;                -- the plan + real timings

SELECT version();
SELECT current_user, current_database(), now();
SELECT pg_size_pretty(pg_database_size('shop'));
SELECT pg_size_pretty(pg_total_relation_size('orders'));

SELECT * FROM pg_stat_activity;            -- who is connected / running what
SELECT pg_terminate_backend(12345);        -- kill a stuck connection by pid

VACUUM ANALYZE orders;
```

---

## 11. Backup and restore (terminal)

```bash
pg_dump shop > shop.sql                    # plain SQL
pg_dump -Fc shop > shop.dump               # compressed custom format
pg_dumpall > all.sql                       # everything, incl. roles

psql shop < shop.sql
pg_restore -d shop shop.dump
```

---

## 12. Service control (Linux)

```bash
sudo systemctl start postgresql
sudo systemctl status postgresql
sudo systemctl restart postgresql

SHOW config_file;                          -- run inside psql to find postgresql.conf
SHOW hba_file;                             -- find pg_hba.conf (login rules)
SELECT pg_reload_conf();                   -- reload config without restart
```

---

### Six mistakes that will cost you an hour each

1. Forgetting the `;` — psql just waits and shows `shop-#`. Type `;` and Enter.
2. `NULL = NULL` is not true. Use `IS NULL` / `IS NOT NULL`.
3. Double quotes `"Name"` mean an identifier. Single quotes `'Name'` mean a string. Never mix them.
4. Unquoted names are folded to lowercase. `CREATE TABLE Users` makes a table called `users`.
5. `DELETE FROM customers` with no `WHERE` deletes everything. There is no undo outside a transaction.
6. `\dt` shows nothing? You are probably in the wrong database (`\c dbname`) or wrong schema (`\dn`, `SET search_path`).
