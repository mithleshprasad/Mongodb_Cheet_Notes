Here's a roadmap for learning MongoDB with Node.js, along with examples to illustrate key concepts:

---

### **1. Understand MongoDB Basics**
- **Learn the fundamentals of MongoDB:**
  - Database, Collection, Document
  - BSON structure (Binary JSON)
  - CRUD Operations (Create, Read, Update, Delete)

#### Example: MongoDB Basics
```json
{
  "name": "John Doe",
  "age": 30,
  "skills": ["JavaScript", "Node.js", "MongoDB"]
}
```

---

### **2. Setup Environment**
- **Install MongoDB:** Download and install MongoDB on your local system or use MongoDB Atlas (cloud-based).
- **Install Node.js:** Ensure Node.js is installed.
- **Install MongoDB Driver for Node.js:**
  ```bash
  npm install mongodb
  ```

---

### **3. Connect Node.js to MongoDB**
- Learn to establish a connection to MongoDB using the official `mongodb` library.

#### Example: Connecting to MongoDB
```javascript
const { MongoClient } = require('mongodb');

const uri = "mongodb://127.0.0.1:27017";
const client = new MongoClient(uri);

async function connect() {
  try {
    await client.connect();
    console.log("Connected to MongoDB!");
  } catch (err) {
    console.error(err);
  } finally {
    await client.close();
  }
}

connect();
```

---

### **4. Perform CRUD Operations**

#### **a. Create Documents**
Learn to insert one or multiple documents into a collection.

Example:
```javascript
const database = client.db("testDB");
const collection = database.collection("users");

await collection.insertOne({ name: "Alice", age: 25 });
await collection.insertMany([
  { name: "Bob", age: 30 },
  { name: "Charlie", age: 35 }
]);
```

---

#### **b. Read Documents**
Learn to query documents using `find`.

Example:
```javascript
const users = await collection.find({ age: { $gte: 30 } }).toArray();
console.log(users);
```

---

#### **c. Update Documents**
Learn to modify existing documents.

Example:
```javascript
await collection.updateOne({ name: "Alice" }, { $set: { age: 26 } });
await collection.updateMany({ age: { $gte: 30 } }, { $set: { active: true } });
```

---

#### **d. Delete Documents**
Learn to remove documents.

Example:
```javascript
await collection.deleteOne({ name: "Alice" });
await collection.deleteMany({ active: true });
```

---

### **5. Use Mongoose for Simplification**
- Install Mongoose for object modeling and schema-based interaction with MongoDB.
  ```bash
  npm install mongoose
  ```

#### Example: Using Mongoose
```javascript
const mongoose = require('mongoose');

mongoose.connect("mongodb://127.0.0.1:27017/testDB", { useNewUrlParser: true, useUnifiedTopology: true });

const userSchema = new mongoose.Schema({
  name: String,
  age: Number,
});

const User = mongoose.model("User", userSchema);

(async () => {
  const user = new User({ name: "Dave", age: 40 });
  await user.save();
  console.log(await User.find());
})();
```

---

### **6. Handle Advanced MongoDB Queries**
- Aggregation Framework
- Indexing for performance
- Pagination and Sorting

#### Example: Aggregation Query
```javascript
const pipeline = [
  { $match: { age: { $gte: 30 } } },
  { $group: { _id: "$age", total: { $sum: 1 } } }
];

const result = await collection.aggregate(pipeline).toArray();
console.log(result);
```

---

### **7. Implement Middleware with Node.js**
- Combine MongoDB operations with Express for creating APIs.

#### Example: Express with MongoDB
```javascript
const express = require('express');
const app = express();

app.use(express.json());

app.get('/users', async (req, res) => {
  const users = await collection.find().toArray();
  res.json(users);
});

app.post('/users', async (req, res) => {
  const newUser = req.body;
  await collection.insertOne(newUser);
  res.json({ message: 'User added' });
});

app.listen(3000, () => console.log("Server running on port 3000"));
```

---

### **8. Learn MongoDB Atlas (Optional)**
- Use MongoDB Atlas for cloud-hosted databases.
- Secure connections with `.env` files and URI strings.

---

### **9. Build a Full-Stack Application**
- Combine MongoDB, Express, React/Angular, and Node.js (MERN/MEAN stack).

---

### **10. Optimize and Secure MongoDB**
- Use indexes for queries.
- Secure MongoDB with authentication and roles.
- Use environment variables for sensitive data like URI.

---

### **11. Explore Advanced Features**
- Transactions in MongoDB
- Change Streams for real-time updates
- GridFS for handling large files

---

### **12. Continuous Practice**
- Build projects:
  - A Blog system with CRUD features
  - A Task Management App
  - An E-commerce API

