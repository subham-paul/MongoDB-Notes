
# MongoDB - Complete Guide 🚀

## Table of Contents
1. [MongoDB Basics](#mongodb-basics)
2. [BSON Explained](#bson-explained)
3. [Key Commands](#key-commands)
4. [Aggregation](#aggregation)
5. [Interview Prep](#interview-prep)
6. [Machine Test Tips](#machine-test-tips)

---

## MongoDB Basics

* **MongoDB** is a **NoSQL**, **document-oriented database**.
* It stores data in **flexible**, **JSON-like** documents (`BSON`).
* Scales horizontally and handles large amounts of unstructured data.

---

### Core Components
- **MongoD** → Database server process (hosts the data)
- **Mongo** → Command-line shell to interact with MongoDB
- **MongoDB Compass** → GUI tool (beginners-friendly alternative)

### SQL vs MongoDB Terminology
| SQL Terms  | MongoDB Terms     |
|------------|-------------------|
| Database   | Database          |
| Tables     | Collections       |
| Rows       | Documents (BSON)  |
| Columns    | Fields            |

---

## BSON Explained

### What is BSON?
- **Binary JSON** - MongoDB's storage format, it optimized for storage & speed.
- Supports **more types** than JSON: `Date`, `Binary`, `ObjectId`, etc.
- Automatically converts JSON → BSON when saving data

### Key Features
✅ **Faster** (binary format)  
✅ **Smaller size** than JSON  
✅ Supports **rich data types**  
✅ **Easily traversable** for queries  

### BSON vs JSON
| Feature        | JSON              | BSON                |
|----------------|-------------------|--------------------|
| Format         | Text-based        | Binary             |
| Speed          | Slower            | Faster             |
| Data Types     | Basic             | Extended           |
| Best For       | APIs/configs      | Databases          |

**Example:**
```javascript
// JSON
{"name": "Alice", "joined": "2023-01-15"}

// BSON (conceptual)
{"name": "Alice", "joined": ISODate("2023-01-15")}
```

---

## ⚡️ MongoDB Shell vs Tools

* **mongod**: Database server process.
* **mongo**: Command-line shell.
* **Compass**: Official MongoDB GUI.
* **Atlas**: MongoDB in the cloud (DBaaS).

---

## Key Commands

### Database Operations
```bash
show dbs                  # List databases
use myDB                  # Create/switch DB
db                        # Current DB
db.dropDatabase()         # Delete current DB
```

### Collection Operations
```bash
show collections                 # List collections
db.createCollection('users')     # Create
db.users.drop()                  # Delete
```

### CRUD Operations
```javascript
// Insert
db.users.insertOne({name: "Alice", age: 25})
db.users.insertMany([{...}, {...}])

// Query
db.users.find().pretty()
db.users.findOne({age: {$gt: 20}})

// Find One
db.comments.findOne({ name: 'Subham' })

// Update
db.users.updateOne({name: "Alice"}, {$set: {age: 26}})

// Upsert
db.comments.update({ name: 'X' }, { $set: { lang: 'JS' } }, { upsert: true })

// Increment
db.comments.update({ name: 'Rohan' }, { $inc: { member_since: 2 } })

// Rename field
db.comments.update({ name: 'Rohan' }, { $rename: { member_since: 'member' } })

// Delete
db.users.deleteOne({name: "Alice"})
```

### Query Operators
```javascript
// Comparison
db.users.find({age: {$lt: 30}})      // Less than
db.users.find({age: {$in: [25,30]}}) // In array

// Logical
db.users.find({$or: [{age: 25}, {name: "Bob"}]})
```

---

## 🔑 Users & Auth

```bash
# Create user
use admin
db.createUser({
  user: "admin",
  pwd: "pass123",
  roles: [{ role: "userAdminAnyDatabase", db: "admin" }]
})
```

---

---
## 🗂️ Data Validation

Enforce schema rules:

```bash
db.createCollection("students", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name", "age"],
      properties: {
        name: { bsonType: "string" },
        age: { bsonType: "int", minimum: 18 }
      }
    }
  }
})
```
---

## ⚙️ ObjectId

* Default `_id` in MongoDB.
* Unique 12-byte ID: timestamp + machine + PID + counter.

```bash
ObjectId("507f1f77bcf86cd799439011")
```

---

## Aggregation Pipeline

### What is Aggregation?
- Multi-stage data processing pipeline
- Used for analytics/transformations

**Common Stages:**
1. `$match` → Filter documents
2. `$group` → Group by field
3. `$sort` → Order results
4. `$project` → Reshape documents by **including**, **excluding**, or **adding fields**
5. `$limit` → Restrict the number of documents returned by the query
6. `$unwind` → To **deconstruct** an array field within a document

**Example:**
```javascript
db.orders.aggregate([
  { $match: { status: "completed" } },
  { $group: { _id: "$product", total: { $sum: "$amount" } } },
  { $sort: { total: -1 } }
])
```

---

## 🔄 Replica Sets (Basics)

* Replica sets = High availability.
* Multiple nodes: 1 primary + 2+ secondaries.
* Auto failover.
* Start with `mongod --replSet`.

---

## ☁️ MongoDB Atlas

* Managed cloud DB.
* Scalable + secure.
* Good for production & practice.

---

## Interview Prep 🔍

### Common Questions
1. **What makes MongoDB different from SQL?**  
   → Document-based vs table-based, schema flexibility, horizontal scaling

2. **When would you use embedded vs referenced documents?**  
   → Embed for 1:few relationships, reference for 1:many

3. **Explain indexing in MongoDB**  
   → Improves query performance (create with `db.col.createIndex({field: 1})`)

4. **What is sharding?**  
   → Horizontal partitioning of data across servers

---

## Machine Test Tips 💻

### What to Expect
1. **CRUD operations** (90% of tests)
2. **Aggregation pipelines** (common for mid-level)
3. **Schema design** (e.g., blog post with comments)
4. **Performance optimization** (indexing, query patterns)

### Practice Tasks
```markdown
1. Create a "products" collection and insert 10 items with price/category
2. Find all products priced $50-$100
3. Calculate average price by category
4. Update stock quantity for a specific product
5. Implement pagination (skip/limit)
```

---
## 🏆 That’s It!
**Pro Tip:** Practice on [MongoDB Playground](https://mongoplayground.net/) for quick experiments! 😊🚀✨

