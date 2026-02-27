# MySQL — referência rápida

*Ligação, queries comuns e boas práticas. Para consulta enquanto trabalhas.*

---

## Ligar à base de dados

### String de conexão (URI)
```
mysql://user:password@host:port/database
```
- Local típico: `mysql://root:password@localhost:3306/nome_da_base`

### Node.js (mysql2)
```javascript
const mysql = require('mysql2/promise');
const pool = mysql.createPool({
  host: 'localhost',
  user: 'root',
  password: process.env.MYSQL_PASSWORD,
  database: 'nome_da_base'
});
// query
const [rows] = await pool.query('SELECT * FROM users WHERE id = ?', [userId]);
```

### Python (mysql-connector ou PyMySQL)
```python
import mysql.connector
conn = mysql.connector.connect(
  host="localhost", user="root", password="...", database="nome_da_base"
)
cursor = conn.cursor(dictionary=True)
cursor.execute("SELECT * FROM users WHERE id = %s", (user_id,))
rows = cursor.fetchall()
```

*Sempre usar parâmetros (?) ou (%s) para evitar SQL injection.*

---

## Queries básicas

| Operação | Exemplo SQL |
|----------|-------------|
| Selecionar | `SELECT id, name, email FROM users WHERE status = 'active'` |
| Inserir | `INSERT INTO users (name, email) VALUES ('Ana', 'ana@mail.com')` |
| Atualizar | `UPDATE users SET name = 'Maria' WHERE id = 1` |
| Apagar | `DELETE FROM users WHERE id = 1` |

### Cláusulas úteis
- **WHERE** — filtro: `WHERE created_at >= '2024-01-01' AND status IN ('a','b')`
- **ORDER BY** — ordenar: `ORDER BY created_at DESC`
- **LIMIT / OFFSET** — paginação: `LIMIT 10 OFFSET 20`
- **JOIN** — juntar tabelas: `FROM orders o JOIN users u ON o.user_id = u.id`
- **GROUP BY** — agrupar: `SELECT category, COUNT(*) FROM products GROUP BY category`
- **HAVING** — filtrar após GROUP BY: `HAVING COUNT(*) > 5`

---

## JOINs em breve

| Tipo | Uso |
|------|-----|
| **INNER JOIN** | Só linhas que existem em ambas as tabelas |
| **LEFT JOIN** | Todas da esquerda; da direita preenche onde houver match |
| **RIGHT JOIN** | O contrário do LEFT |
| **CROSS JOIN** | Produto cartesiano (cuidado com tamanho) |

### Exemplo
```sql
SELECT u.name, o.total
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
WHERE u.country = 'PT';
```

---

## Índices e desempenho

- **Criar índice:** `CREATE INDEX idx_email ON users(email);`
- **Índice único:** `CREATE UNIQUE INDEX idx_email ON users(email);`
- **Compound:** `CREATE INDEX idx_status_created ON orders(status, created_at);`
- **Ver índices:** `SHOW INDEX FROM users;`

*Índices em colunas usadas em WHERE, JOIN e ORDER BY melhoram muito a velocidade.*

---

## Transações

```sql
START TRANSACTION;
-- várias queries
INSERT INTO ...;
UPDATE ...;
COMMIT;   -- confirma
-- ou
ROLLBACK; -- desfaz tudo
```

Em código (Node com mysql2): usar `connection.beginTransaction()`, `commit()` e `rollback()` na mesma conexão.

---

## Diferenças rápidas: MySQL vs MongoDB

| Aspeto | MySQL | MongoDB |
|--------|--------|---------|
| Modelo | Tabelas e linhas (relacional) | Coleções e documentos (JSON-like) |
| Schema | Definido (colunas, tipos) | Flexível (pode variar por documento) |
| Queries | SQL | Métodos/operadores e aggregation pipeline |
| Joins | JOIN em SQL | $lookup em agregação ou aplicação |
| Transações | Suportadas | Suportadas (recentes em replicasets) |

*Escolhe MySQL quando a estrutura for estável e relações entre tabelas forem centrais; MongoDB quando os dados forem mais variados ou hierárquicos.*

---

*Podes acrescentar aqui queries teus, nomes de bases/tabelas e scripts de migração.*
