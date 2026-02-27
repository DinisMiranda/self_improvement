# MySQL — quick reference

*Connection, common queries, and best practices. For lookup while you work.*

---

## Connecting to the database

### Connection string (URI)
```
mysql://user:password@host:port/database
```
- Typical local: `mysql://root:password@localhost:3306/db_name`

### Node.js (mysql2)
```javascript
const mysql = require('mysql2/promise');
const pool = mysql.createPool({
  host: 'localhost',
  user: 'root',
  password: process.env.MYSQL_PASSWORD,
  database: 'db_name'
});
// query
const [rows] = await pool.query('SELECT * FROM users WHERE id = ?', [userId]);
```

### Python (mysql-connector or PyMySQL)
```python
import mysql.connector
conn = mysql.connector.connect(
  host="localhost", user="root", password="...", database="db_name"
)
cursor = conn.cursor(dictionary=True)
cursor.execute("SELECT * FROM users WHERE id = %s", (user_id,))
rows = cursor.fetchall()
```

*Always use parameters (?) or (%s) to avoid SQL injection.*

---

## Basic queries

| Operation | Example SQL |
|-----------|-------------|
| Select | `SELECT id, name, email FROM users WHERE status = 'active'` |
| Insert | `INSERT INTO users (name, email) VALUES ('Ana', 'ana@mail.com')` |
| Update | `UPDATE users SET name = 'Maria' WHERE id = 1` |
| Delete | `DELETE FROM users WHERE id = 1` |

### Useful clauses
- **WHERE** — filter: `WHERE created_at >= '2024-01-01' AND status IN ('a','b')`
- **ORDER BY** — sort: `ORDER BY created_at DESC`
- **LIMIT / OFFSET** — pagination: `LIMIT 10 OFFSET 20`
- **JOIN** — join tables: `FROM orders o JOIN users u ON o.user_id = u.id`
- **GROUP BY** — group: `SELECT category, COUNT(*) FROM products GROUP BY category`
- **HAVING** — filter after GROUP BY: `HAVING COUNT(*) > 5`

---

## JOINs in brief

| Type | Use |
|------|-----|
| **INNER JOIN** | Only rows that exist in both tables |
| **LEFT JOIN** | All from left; right fills in where there's a match |
| **RIGHT JOIN** | Opposite of LEFT |
| **CROSS JOIN** | Cartesian product (watch size) |

### Example
```sql
SELECT u.name, o.total
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
WHERE u.country = 'PT';
```

---

## Indexes and performance

- **Create index:** `CREATE INDEX idx_email ON users(email);`
- **Unique index:** `CREATE UNIQUE INDEX idx_email ON users(email);`
- **Compound:** `CREATE INDEX idx_status_created ON orders(status, created_at);`
- **List indexes:** `SHOW INDEX FROM users;`

*Indexes on columns used in WHERE, JOIN, and ORDER BY greatly improve speed.*

---

## Transactions

```sql
START TRANSACTION;
-- several queries
INSERT INTO ...;
UPDATE ...;
COMMIT;   -- confirm
-- or
ROLLBACK; -- undo all
```

In code (Node with mysql2): use `connection.beginTransaction()`, `commit()`, and `rollback()` on the same connection.

---

## Quick comparison: MySQL vs MongoDB

| Aspect | MySQL | MongoDB |
|--------|--------|---------|
| Model | Tables and rows (relational) | Collections and documents (JSON-like) |
| Schema | Defined (columns, types) | Flexible (can vary per document) |
| Queries | SQL | Methods/operators and aggregation pipeline |
| Joins | JOIN in SQL | $lookup in aggregation or in app |
| Transactions | Supported | Supported (recent in replicasets) |

*Choose MySQL when structure is stable and table relationships are central; MongoDB when data is more varied or hierarchical.*

---

*You can add your own queries, database/table names, and migration scripts here.*
