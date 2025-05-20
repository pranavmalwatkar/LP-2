Here’s a clean and simple implementation for both parts using MongoDB syntax and Python with `pymongo`.

---

### **a. Implement Map-Reduce Operation using MongoDB**

**Goal**: Count the total marks for each student.

```javascript
// Sample MongoDB collection: students
db.students.insertMany([
  { name: "Alice", subject: "Math", marks: 80 },
  { name: "Alice", subject: "Science", marks: 75 },
  { name: "Bob", subject: "Math", marks: 90 },
  { name: "Bob", subject: "Science", marks: 85 }
]);

// Map function
var mapFunction = function () {
  emit(this.name, this.marks);
};

// Reduce function
var reduceFunction = function (key, values) {
  return Array.sum(values);
};

// Execute MapReduce
db.students.mapReduce(
  mapFunction,
  reduceFunction,
  { out: "total_marks" }
);

// View result
db.total_marks.find();
```

---

### **b. MongoDB Queries using Aggregation and Indexing**

#### **1. Aggregation: Total marks per student**

```javascript
db.students.aggregate([
  {
    $group: {
      _id: "$name",
      totalMarks: { $sum: "$marks" }
    }
  }
]);
```

#### **2. Aggregation: Average marks per subject**

```javascript
db.students.aggregate([
  {
    $group: {
      _id: "$subject",
      avgMarks: { $avg: "$marks" }
    }
  }
]);
```

#### **3. Create an Index on `name` field**

```javascript
db.students.createIndex({ name: 1 });
```

#### **4. Find student by name using index**

```javascript
db.students.find({ name: "Alice" });
```

---

Let me know if you want the same in Python with `pymongo` or for a different use case.
