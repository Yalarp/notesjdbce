# MongoDB Integration with Node.js

## Table of Contents
1. [Introduction](#1-introduction)
2. [MongoDB Basics](#2-mongodb-basics)
3. [Mongoose ODM](#3-mongoose-odm)
4. [CRUD Operations](#4-crud-operations)
5. [Schemas and Models](#5-schemas-and-models)
6. [Queries and Filters](#6-queries-and-filters)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 What is MongoDB?
**MongoDB** is a NoSQL document database that stores data in flexible, JSON-like documents (BSON). It's designed for scalability and flexibility.

### 1.2 Key Features
- Document-oriented storage
- Flexible schema
- Horizontal scalability
- Rich query language
- Indexing support

### 1.3 SQL vs MongoDB

| SQL | MongoDB |
|-----|---------|
| Table | Collection |
| Row | Document |
| Column | Field |
| Primary Key | _id |
| JOIN | $lookup |

---

## 2. MongoDB Basics

### 2.1 Installation

```bash
# Install MongoDB driver
npm install mongodb

# Install Mongoose (recommended)
npm install mongoose
```

### 2.2 Connecting with Native Driver

```javascript
const { MongoClient } = require('mongodb');

const uri = 'mongodb://localhost:27017';
const client = new MongoClient(uri);

async function connect() {
    try {
        await client.connect();
        console.log('Connected to MongoDB');
        
        const db = client.db('myapp');
        const collection = db.collection('users');
        
        // Use collection...
        
    } finally {
        await client.close();
    }
}

connect();
```

---

## 3. Mongoose ODM

### 3.1 What is Mongoose?
Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js. It provides schema-based solution with built-in validation.

### 3.2 Connecting with Mongoose

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/myapp', {
    useNewUrlParser: true,
    useUnifiedTopology: true
})
.then(() => console.log('MongoDB connected'))
.catch(err => console.error('Connection error:', err));
```

### 3.3 Connection Events

```javascript
const mongoose = require('mongoose');

mongoose.connection.on('connected', () => {
    console.log('Mongoose connected');
});

mongoose.connection.on('error', (err) => {
    console.error('Mongoose error:', err);
});

mongoose.connection.on('disconnected', () => {
    console.log('Mongoose disconnected');
});
```

---

## 4. CRUD Operations

### 4.1 Create

```javascript
// Create one
const user = new User({ name: 'John', email: 'john@test.com' });
await user.save();

// Or using create()
const newUser = await User.create({
    name: 'Jane',
    email: 'jane@test.com'
});

// Create many
await User.insertMany([
    { name: 'User1', email: 'u1@test.com' },
    { name: 'User2', email: 'u2@test.com' }
]);
```

### 4.2 Read

```javascript
// Find all
const users = await User.find();

// Find with conditions
const activeUsers = await User.find({ status: 'active' });

// Find one
const user = await User.findOne({ email: 'john@test.com' });

// Find by ID
const userById = await User.findById('60abc123def456...');

// Find with specific fields
const names = await User.find().select('name email');

// Limit and skip
const paginatedUsers = await User.find()
    .skip(0)
    .limit(10);
```

### 4.3 Update

```javascript
// Update one
await User.updateOne(
    { _id: userId },
    { $set: { name: 'Updated Name' } }
);

// Find and update
const updated = await User.findByIdAndUpdate(
    userId,
    { name: 'New Name' },
    { new: true }  // Return updated document
);

// Update many
await User.updateMany(
    { status: 'inactive' },
    { $set: { status: 'active' } }
);
```

### 4.4 Delete

```javascript
// Delete one
await User.deleteOne({ _id: userId });

// Find and delete
const deleted = await User.findByIdAndDelete(userId);

// Delete many
await User.deleteMany({ status: 'inactive' });
```

---

## 5. Schemas and Models

### 5.1 Defining a Schema

```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
    name: {
        type: String,
        required: [true, 'Name is required'],
        minlength: 2,
        maxlength: 50
    },
    email: {
        type: String,
        required: true,
        unique: true,
        lowercase: true
    },
    age: {
        type: Number,
        min: 0,
        max: 120
    },
    role: {
        type: String,
        enum: ['user', 'admin', 'moderator'],
        default: 'user'
    },
    isActive: {
        type: Boolean,
        default: true
    },
    createdAt: {
        type: Date,
        default: Date.now
    }
});

const User = mongoose.model('User', userSchema);
module.exports = User;
```

### 5.2 Schema Types

| Type | Description |
|------|-------------|
| String | Text data |
| Number | Numeric data |
| Date | Date/time |
| Boolean | true/false |
| ObjectId | Reference to other document |
| Array | List of values |
| Mixed | Any type |
| Buffer | Binary data |

### 5.3 Schema Options

```javascript
const userSchema = new mongoose.Schema({
    name: String,
    email: String
}, {
    timestamps: true,       // Adds createdAt, updatedAt
    collection: 'users',    // Collection name
    versionKey: false       // Disable __v field
});
```

### 5.4 Virtual Fields

```javascript
userSchema.virtual('fullName').get(function() {
    return `${this.firstName} ${this.lastName}`;
});
```

### 5.5 Instance Methods

```javascript
userSchema.methods.isAdmin = function() {
    return this.role === 'admin';
};

// Usage
const user = await User.findById(id);
if (user.isAdmin()) {
    // ...
}
```

### 5.6 Static Methods

```javascript
userSchema.statics.findByEmail = function(email) {
    return this.findOne({ email });
};

// Usage
const user = await User.findByEmail('john@test.com');
```

---

## 6. Queries and Filters

### 6.1 Query Operators

```javascript
// Comparison
{ age: { $gt: 18 } }      // Greater than
{ age: { $gte: 18 } }     // Greater than or equal
{ age: { $lt: 65 } }      // Less than
{ age: { $lte: 65 } }     // Less than or equal
{ age: { $ne: 30 } }      // Not equal
{ status: { $in: ['active', 'pending'] } }  // In array
{ status: { $nin: ['deleted'] } }           // Not in array

// Logical
{ $and: [{ age: { $gt: 18 } }, { status: 'active' }] }
{ $or: [{ status: 'active' }, { role: 'admin' }] }
{ status: { $not: { $eq: 'deleted' } } }
```

### 6.2 Query Methods

```javascript
// Chained queries
const users = await User.find()
    .where('age').gt(18)
    .where('status').equals('active')
    .select('name email')
    .sort('-createdAt')
    .limit(10)
    .skip(0);
```

### 6.3 Population (References)

```javascript
// Schema with reference
const postSchema = new mongoose.Schema({
    title: String,
    author: {
        type: mongoose.Schema.Types.ObjectId,
        ref: 'User'
    }
});

// Populate reference
const posts = await Post.find()
    .populate('author', 'name email');
```

### 6.4 Aggregation

```javascript
const stats = await User.aggregate([
    { $match: { status: 'active' } },
    { $group: {
        _id: '$role',
        count: { $sum: 1 },
        avgAge: { $avg: '$age' }
    }},
    { $sort: { count: -1 } }
]);
```

---

## 7. Quick Reference

### 7.1 Connection

```javascript
mongoose.connect('mongodb://localhost:27017/dbname');
```

### 7.2 Schema

```javascript
const schema = new mongoose.Schema({
    field: { type: String, required: true }
});
const Model = mongoose.model('Name', schema);
```

### 7.3 CRUD

```javascript
// Create
await Model.create(data);

// Read
await Model.find(filter);
await Model.findById(id);
await Model.findOne(filter);

// Update
await Model.findByIdAndUpdate(id, update, { new: true });

// Delete
await Model.findByIdAndDelete(id);
```

### 7.4 Query Operators

```javascript
$eq, $ne, $gt, $gte, $lt, $lte
$in, $nin
$and, $or, $not
$exists, $type
$regex
```

---

## 8. Interview Questions

### Q1: What is MongoDB?
**Answer**: MongoDB is a NoSQL document database that stores data in flexible, JSON-like documents called BSON. It's schema-less and horizontally scalable.

### Q2: What is Mongoose?
**Answer**: Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js. It provides schema-based modeling, validation, middleware, and more.

### Q3: What is the difference between find() and findOne()?
**Answer**:
- `find()`: Returns an array of all matching documents
- `findOne()`: Returns only the first matching document

### Q4: What is population in Mongoose?
**Answer**: Population is the process of replacing ObjectId references with actual documents from another collection. It's similar to a JOIN in SQL.

### Q5: What are Mongoose middleware/hooks?
**Answer**: Middleware are functions that run at specific stages (pre/post) of operations like save, validate, remove. Used for validation, logging, etc.

### Q6: What is the difference between save() and create()?
**Answer**:
- `save()`: Instance method, works on a document
- `create()`: Model method, combines new Model() and save()

---

## Navigation

← Previous: [39_REST_API_Development.md](./39_REST_API_Development.md) | Next: [41_React_Introduction.md](../Module_06_React_Basics/41_React_Introduction.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 08*
