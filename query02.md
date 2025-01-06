# MongoDB Practice Tasks


```javascript


// Task 1: Add multiple students

db.students.insertMany([
  {
    name: "Mahir Patel",
    roll_number: "ECE2002",
    department: "Electronics",
    year: 1,
    courses_enrolled: ["Circuit Analysis", "Digital Systems"]
  },
  {
    name: "Rohit Chaudhary",
    roll_number: "CSE1003",
    department: "Computer Science",
    year: 3,
    courses_enrolled: ["MongoDB", "NodeJS"]
  },
  {
    name: "Jenil kumar",
    roll_number: "CSE1004",
    department: "Computer Science",
    year: 2,
    courses_enrolled: ["NodeJS", "React"]
  }
  {
    name: "Kalpan kumar",
    roll_number: "CSE1004",
    department: "Computer Science",
    year: 2,
    courses_enrolled: ["Mongo", "React"]
  }
  {
    name: "Dev Patel",
    roll_number: "CSE1004",
    department: "Computer Science",
    year: 2,
    courses_enrolled: ["NodeJS", "React"]
  }
]);



// Task 2: Add multiple subjects

db.subjects.insertMany([
  {
    name: "NodeJS",
    topics: ["Express", "API Creation", "Middleware"]
  },
  {
    name: "React",
    topics: ["JSX", "State Management", "Lifecycle Methods"]
  },
  {
    name: "MongoDB",
    topics: ["CRUD Operations", "Aggregation", "Indexing"]
  },
  {
    name: "Environmental Science",
    topics: ["Ecology", "Physic", "Chemistry"]
  },
]);



// Task 3: Query students based on subject enrollment

db.students.find({ courses_enrolled: "NodeJS" });



// Task 4: Add a new topic to a subject

db.subjects.updateOne(
  { name: "NodeJS" },
  { $push: { topics: "Error Handling" } }
);



// Task 5: Query subjects with multiple topics

db.subjects.find({ $expr: { $gte: [{ $size: "$topics" }, 4] } });



// Task 6: Update student enrollment

db.students.updateOne(
  { name: "Jenil Kumar" },
  { $push: { courses_enrolled: "React Native" } }
);



// Task 7: Query all students

db.students.find({}, { name: 1, courses_enrolled: 1, _id: 0 });



// Task 8: Update multiple students' year

db.students.updateMany(
  { department: "Computer Science" },
  { $set: { year: 3 } }
);



// Task 9: Add new topics to multiple subjects

db.subjects.updateOne(
  { name: "React" },
  { $push: { topics: "Hooks" } }
);
db.subjects.updateOne(
  { name: "NodeJS" },
  { $push: { topics: "Authentication" } }
);
db.subjects.updateOne(
  { name: "MongoDB" },
  { $push: { topics: "Replication" } }
);



// Task 10: Remove a topic from a subject

db.subjects.updateOne(
  { name: "NodeJS" },
  { $pull: { topics: "Express" } }
);



// Task 11: Query all students in a specific year

db.students.find({ year: { $in: [2, 3] } });



// Task 12: Delete a student by roll number

db.students.deleteOne({ roll_number: "CSE1003" });



// Task 13: Delete all students from a department

db.students.deleteMany({ department: "Electrical Engineering" });



// Task 14: Retrieve all topics for a subject

db.subjects.find({ name: "MongoDB" }, { topics: 1, _id: 0 });



// Task 15: Count the number of subjects in which a student is enrolled

db.students.aggregate([
  {
    $project: {
      name: 1,
      courses_count: { $size: "$courses_enrolled" }
    }
  }
]);
