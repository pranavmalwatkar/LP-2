# LP-2
db.students.insertMany([
  {
    name: "Alice",
    age: 22,
    courses: ["Math", "Science", "History"]
  },
  {
    name: "Bob",
    age: 19,
    courses: ["Math", "English"]
  },
  {
    name: "Charlie",
    age: 24,
    courses: ["Physics", "Chemistry", "Biology", "Math"]
  },
  {
    name: "David",
    age: 21,
    courses: ["Geography", "Economics"]
  },
  {
    name: "Alice",
    age: 22,
    courses: ["Computer Science"] // Another entry for same name to test MapReduce
  }
]);


  aggregation:
db.students.aggregate([
  {
    $project: {
      name: 1,
      courseCount: {
        $cond: {
          if: { $isArray: "$courses" },
          then: { $size: "$courses" },
          else: 0
        }
      }
    }
  },
  {
    $group: {
      _id: "$name",
      totalCourses: { $sum: "$courseCount" }
    }
  }
]);
