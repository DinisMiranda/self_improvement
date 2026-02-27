# MongoDB — quick reference

*Connection, CRUD, aggregations, and indexes. For lookup while you work.*

---

## Connecting to the database

### Connection string (URI)
```
mongodb://user:password@host:port/database?options
```
- No auth (local): `mongodb://localhost:27017`
- With specific database: `mongodb://localhost:27017/db_name`

### Node.js (official driver)
```javascript
const { MongoClient } = require('mongodb');
const client = new MongoClient(process.env.MONGODB_URI);

async function run() {
  await client.connect();
  const db = client.db('db_name');
  const collection = db.collection('users');
  // ...
  await client.close();
}
```

### Python (PyMongo)
```python
from pymongo import MongoClient
client = MongoClient("mongodb://localhost:27017/")
db = client["db_name"]
collection = db["users"]
```

---

## Basic CRUD

| Operation | Method (Node) | Example |
|-----------|----------------|---------|
| Insert one | `insertOne(doc)` | `collection.insertOne({ name: "Ana", age: 30 })` |
| Insert many | `insertMany([...])` | `collection.insertMany([{ a: 1 }, { a: 2 }])` |
| Find one | `findOne(filter)` | `collection.findOne({ name: "Ana" })` |
| Find many | `find(filter)` | `collection.find({ age: { $gte: 18 } })` |
| Update one | `updateOne(filter, update)` | `collection.updateOne({ _id }, { $set: { name: "Maria" } })` |
| Update many | `updateMany(filter, update)` | `collection.updateMany({ status: "old" }, { $set: { status: "new" } })` |
| Delete one | `deleteOne(filter)` | `collection.deleteOne({ _id })` |
| Delete many | `deleteMany(filter)` | `collection.deleteMany({ status: "deleted" })` |

### Useful query operators
- **`$eq`** — equal | **`$ne`** — not equal  
- **`$gt`**, **`$gte`**, **`$lt`**, **`$lte`** — comparisons  
- **`$in`** — value in list: `{ status: { $in: ["active", "pending"] } }`  
- **`$exists`** — field exists: `{ email: { $exists: true } }`  
- **`$regex`** — text: `{ name: { $regex: /ana/i } }`

### Update operators
- **`$set`** — set/overwrite fields  
- **`$unset`** — remove field  
- **`$inc`** — increment (e.g. counters)  
- **`$push`** / **`$pull`** — add/remove from arrays  

---

## Aggregations (aggregation pipeline)

Pipeline = sequence of stages. Each stage transforms the documents.

| Stage | Use |
|-------|-----|
| **`$match`** | Filter documents (like `find`) |
| **`$group`** | Group and aggregate (count, sum, avg) |
| **`$sort`** | Sort |
| **`$project`** | Select/rename fields |
| **`$lookup`** | "Join" with another collection |
| **`$unwind`** | Expand an array into multiple documents |
| **`$limit`** / **`$skip`** | Pagination |

### Example: count by category
```javascript
collection.aggregate([
  { $match: { status: "active" } },
  { $group: { _id: "$category", total: { $sum: 1 } } },
  { $sort: { total: -1 } }
]);
```

---

## Indexes

- **Create:** `collection.createIndex({ field: 1 })` — 1 = ascending, -1 = descending.
- **Unique:** `createIndex({ email: 1 }, { unique: true })`.
- **Compound:** `createIndex({ category: 1, createdAt: -1 })` — useful for queries filtering on both.
- **List indexes:** `collection.indexes()`.

*Without an index on fields you use in `find` or `$match`, queries can be slow on large collections.*

---

## Quick tips

- **`_id`** — MongoDB creates it automatically if you don't provide one; you can use `ObjectId` or your own value (e.g. string).
- **Projection:** to return only some fields: `find({}, { name: 1, email: 1, _id: 0 })`.
- **Cursor:** `find()` returns a cursor; in Node use `.toArray()` or iterate with `for await`.
- **Transactions:** for multiple operations in one transaction, use `client.startSession()` and `session.withTransaction(...)`.

*You can add your own examples (projects, schemas, pipelines) as you use them.*
