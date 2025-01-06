# MongoDB Additional Practice Assignment



```javascript


// Task 1: Additional Questions on CRUD Operations

// Insert new students into the "students" collection
db.students.insertMany([
  {
    name: "Dev Patel",
    roll_number: "CSE1010",
    department: "Computer Science",
    year: 1,
    courses_enrolled: ["CS101", "CS102", "Math101"]
  },
  {
    name: "Dharti Raval",
    roll_number: "ECE3005",
    department: "Electronics",
    year: 3,
    courses_enrolled: ["EC201", "CS101"]
  }
]);



// Update the department of a student based on their roll number

db.students.updateOne(
  { roll_number: "CSE1010" },
  { $set: { department: "Information Technology" } }
);



// Remove all students who have enrolled in less than 3 courses

db.students.deleteMany({
  $expr: { $lt: [{ $size: "$courses_enrolled" }, 3] }
});



// Task 2: Aggregation Exercise


db.students.aggregate([
  {
    $group: {
      _id: "$department",
      student_count: { $sum: 1 }
    }
  },
  {
    $sort: { student_count: -1 }
  },
  {
    $limit: 1
  }
]);



// Task 3: Advanced Querying Exercise

db.students.find({
  courses_enrolled: { $all: ["CS101", "Math101"] }
});



// Task 4: Indexing and Performance


db.students.createIndex({ department: 1 });

db.students.createIndex({ year: 1 });

db.students.find({ department: "Computer Science" }).explain("executionStats");
