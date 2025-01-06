# MongoDB Practice Assignments

```javascript
// Task - 1: Create Database and Collections


use CodingGitaStudents;
db.createCollection("students");
db.createCollection("courses");



// 1
db.students.insertMany([
  {
    name: "Nisarg Patel",
    roll_number: "CSE1001",
    department: "Computer Science",
    year: 2,
    courses_enrolled: ["CS101", "CS102"]
  },
  {
    name: "Janvi Patel",
    roll_number: "ECE2001",
    department: "Electronics",
    year: 1,
    courses_enrolled: ["EC101", "CS101"]
  }
]);


// 2
db.courses.insertMany([
  {
    course_code: "CS101",
    name: "Introduction to Programming",
    credits: 4,
    instructor: "Neel Patel"
  },
  {
    course_code: "CS102",
    name: "Data Structures",
    credits: 3,
    instructor: "Dr. Kavita Sharma"
  }
]);




// Task - 2: Perform CRUD Operations


db.students.insertOne({
  name: "Anand Kumar",
  roll_number: "ME3001",
  department: "Mechanical",
  year: 3,
  courses_enrolled: ["ME101", "CS101"]
});
db.courses.insertOne({
  course_code: "ME101",
  name: "Thermodynamics",
  credits: 3,
  instructor: "Dr. Rajivkumar Sharma"
});


// Query 
db.students.find({ department: "Computer Science" });
db.students.find({ year: 2 });
db.students.find({ courses_enrolled: "CS101" });


db.students.updateOne(
  { roll_number: "CSE1001" },
  { $push: { courses_enrolled: "CS103" } }
);


db.students.deleteOne({ roll_number: "ME3001" });
db.courses.deleteOne({ course_code: "ME101" });




