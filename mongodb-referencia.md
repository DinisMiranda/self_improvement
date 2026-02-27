# MongoDB — referência rápida

*Ligação, CRUD, agregações e índices. Para consulta enquanto trabalhas.*

---

## Ligar à base de dados

### String de conexão (URI)
```
mongodb://user:password@host:port/database?options
```
- Sem autenticação (local): `mongodb://localhost:27017`
- Com base específica: `mongodb://localhost:27017/nome_da_base`

### Node.js (driver oficial)
```javascript
const { MongoClient } = require('mongodb');
const client = new MongoClient(process.env.MONGODB_URI);

async function run() {
  await client.connect();
  const db = client.db('nome_da_base');
  const collection = db.collection('users');
  // ...
  await client.close();
}
```

### Python (PyMongo)
```python
from pymongo import MongoClient
client = MongoClient("mongodb://localhost:27017/")
db = client["nome_da_base"]
collection = db["users"]
```

---

## CRUD básico

| Operação | Método (Node) | Exemplo |
|----------|----------------|---------|
| Inserir um | `insertOne(doc)` | `collection.insertOne({ name: "Ana", age: 30 })` |
| Inserir vários | `insertMany([...])` | `collection.insertMany([{ a: 1 }, { a: 2 }])` |
| Buscar um | `findOne(filter)` | `collection.findOne({ name: "Ana" })` |
| Buscar vários | `find(filter)` | `collection.find({ age: { $gte: 18 } })` |
| Atualizar um | `updateOne(filter, update)` | `collection.updateOne({ _id }, { $set: { name: "Maria" } })` |
| Atualizar vários | `updateMany(filter, update)` | `collection.updateMany({ status: "old" }, { $set: { status: "new" } })` |
| Apagar um | `deleteOne(filter)` | `collection.deleteOne({ _id })` |
| Apagar vários | `deleteMany(filter)` | `collection.deleteMany({ status: "deleted" })` |

### Operadores úteis em queries
- **`$eq`** — igual | **`$ne`** — diferente  
- **`$gt`**, **`$gte`**, **`$lt`**, **`$lte`** — comparações  
- **`$in`** — valor em lista: `{ status: { $in: ["active", "pending"] } }`  
- **`$exists`** — campo existe: `{ email: { $exists: true } }`  
- **`$regex`** — texto: `{ name: { $regex: /ana/i } }`

### Operadores de update
- **`$set`** — definir/sobrescrever campos  
- **`$unset`** — remover campo  
- **`$inc`** — incrementar (ex.: contadores)  
- **`$push`** / **`$pull`** — adicionar/remover de arrays  

---

## Agregações (aggregation pipeline)

Pipeline = sequência de estágios. Cada estágio transforma os documentos.

| Estágio | Uso |
|---------|-----|
| **`$match`** | Filtrar documentos (como um `find`) |
| **`$group`** | Agrupar e fazer contas (count, sum, avg) |
| **`$sort`** | Ordenar |
| **`$project`** | Escolher/renomear campos |
| **`$lookup`** | “Join” com outra collection |
| **`$unwind`** | Expandir um array em vários documentos |
| **`$limit`** / **`$skip`** | Paginação |

### Exemplo: contar por categoria
```javascript
collection.aggregate([
  { $match: { status: "active" } },
  { $group: { _id: "$category", total: { $sum: 1 } } },
  { $sort: { total: -1 } }
]);
```

---

## Índices

- **Criar:** `collection.createIndex({ campo: 1 })` — 1 = ascendente, -1 = descendente.
- **Único:** `createIndex({ email: 1 }, { unique: true })`.
- **Compound:** `createIndex({ category: 1, createdAt: -1 })` — útil para queries que filtram por ambos.
- **Ver índices:** `collection.indexes()`.

*Sem índice em campos que usas em `find` ou `$match`, as queries podem ficar lentas em coleções grandes.*

---

## Dicas rápidas

- **`_id`** — MongoDB cria automaticamente se não passares; podes usar `ObjectId` ou um valor teu (ex.: string).
- **Projeção:** para trazer só alguns campos: `find({}, { name: 1, email: 1, _id: 0 })`.
- **Cursor:** `find()` devolve um cursor; em Node usa `.toArray()` ou itera com `for await`.
- **Transações:** para várias operações numa só transação, usa `client.startSession()` e `session.withTransaction(...)`.

*Podes acrescentar aqui exemplos teus (projetos, schemas, pipelines) à medida que fores usando.*
