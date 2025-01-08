# MongoDB Practice Assignment



```javascript


// Task 1: Add more students to the students collection

db.students.insertMany([
  {
    name: "Akash Sharma",
    roll_number: "CSE1005",
    department: "Computer Science",
    year: 1,
    courses_enrolled: ["CS101", "MATH101"]
  },
  {
    name: "Riya Gupta",
    roll_number: "ECE2003",
    department: "Electronics",
    year: 2,
    courses_enrolled: ["EC102", "CS101"]
  },
  {
    name: "Vikas Singh",
    roll_number: "ME3003",
    department: "Mechanical",
    year: 3,
    courses_enrolled: ["ME201", "MATH101"]
  },
  {
    name: "Priya Desai",
    roll_number: "CSE1006",
    department: "Computer Science",
    year: 2,
    courses_enrolled: ["CS102", "CS101"]
  },
  {
    name: "Anil Mehta",
    roll_number: "CIV4001",
    department: "Civil Engineering",
    year: 4,
    courses_enrolled: ["CE301", "MATH101"]
  }
]);



// Task 2: Insert a new course into the courses collection

db.courses.insertOne({
  course_code: "CS202",
  name: "Data Structures",
  credits: 3,
  instructor: "Prof. Krishna"
});



// Task 3: Fetch a specific student's record by roll number

db.students.find({ roll_number: "CSE1002" });



// Task 4: Query all students who are enrolled in a particular course

db.students.find({ courses_enrolled: "MATH101" });



// Task 5: Update a student's courses

db.students.updateOne(
  { roll_number: "CSE1001" },
  { $push: { courses_enrolled: "CS202" } }
);



// Task 6: Remove a course from a student's courses list

db.students.updateOne(
  { name: "Mahir" },
  { $pull: { courses_enrolled: "MATH101" } }
);



// Task 7: Find all courses with 3 credits

db.courses.find({ credits: 3 });



// Task 8: Find students who have enrolled in more than 2 courses

db.students.find({
  $expr: { $gt: [{ $size: "$courses_enrolled" }, 2] }
});



// Task 9: Use the $in operator to find students enrolled in multiple courses

db.students.find({
  courses_enrolled: { $in: ["CS101", "MATH202"] }
});



// Task 10: Fetch all students from a specific department (e.g., CSE)

db.students.find({ department: "CSE" });



// Task 11: Query students who are in their 3rd year

db.students.find({ year: 3 });



// Task 12: Query students using a range for their year

db.students.find({ year: { $gte: 2, $lte: 3 } });



// Task 13: Count the total number of students in each department

db.students.aggregate([
  { $group: { _id: "$department", totalStudents: { $sum: 1 } } }
]);



// Task 14: Group courses by credits

db.courses.aggregate([
  { $group: { _id: "$credits", totalCourses: { $sum: 1 } } }
]);



// Task 15: Find the highest credit course

db.courses.find().sort({ credits: -1 }).limit(1);



// Task 16: Use the $and operator for filtering students

db.students.find({
  $and: [
    { department: "CSE" },
    { $expr: { $gt: [{ $size: "$courses_enrolled" }, 2] } }
  ]
});



// Task 17: Add a new field to all documents in the students collection

db.students.updateMany({}, { $set: { activeStatus: true } });



// Task 18: Use $rename to rename a field

db.students.updateMany({}, { $rename: { courses_enrolled: "enrolledCourses" } });



// Task 19: Set default values for new fields in all student documents

db.students.updateMany({}, { $set: { graduationYear: 2025 } });



// Task 20: Use the $push operator to add a new course to a student’s course list

db.students.updateOne(
  { name: "Mahir" },
  { $push: { enrolledCourses: "CS303" } }
);



// Task 21: Use $pull to remove a course from a student's courses list

db.students.updateOne(
  { name: "Jenil" },
  { $pull: { enrolledCourses: "CS101" } }
);



// Task 22: Remove a student from the students collection

db.students.deleteOne({ roll_number: "CS1004" });



// Task 23: Find students who are enrolled in both CS101 and MATH202

db.students.find({ enrolledCourses: { $all: ["CS101", "MATH202"] } });



// Task 24: Use $regex to search for students whose name starts with "A"

db.students.find({ name: { $regex: "^A", $options: "i" } });



// Task 25: Use $exists to find students with enrolled courses

db.students.find({ enrolledCourses: { $exists: true, $ne: [] } });



// Task 26: Add a field to store students' grades for each course

db.students.updateMany({}, { $set: { grades: [] } });



// Task 27: Use $elemMatch to query students enrolled in specific courses

db.students.find({
  grades: {
    $elemMatch: { course: "CS101", grade: "A" }
  }
});



// Task 28: Use $size operator to query students with exactly 2 courses enrolled

db.students.find({ enrolledCourses: { $size: 2 } });



// Task 29: Perform a text search for a course title

db.courses.createIndex({ name: "text" });
db.courses.find({ $text: { $search: "Digital Electronics" } });



// Task 30: Create a compound index on department and year

db.students.createIndex({ department: 1, year: 1 });



// Task 31: Use $sort to order students by their roll number

db.students.find().sort({ roll_number: 1 });



// Task 32: Create a unique index on the roll number

db.students.createIndex({ roll_number: 1 }, { unique: true });



// Task 33: Update the course name in the courses collection

db.courses.updateOne(
  { course_code: "CS101" },
  { $set: { name: "Intro to Programming" } }
);



// Task 34: Create a backup of the CodingGitaStudents database

 mongodump --db CodingGitaStudents --out /path/to/backup/directory



// Task 35: Restore the CodingGitaStudents database from the backup

 mongorestore --db CodingGitaStudents /path/to/backup/directory/CodingGitaStudents



// Task 36: Use $project to reshape data in aggregation

db.students.aggregate([
  {
    $project: {
      _id: 0,
      name: 1,
      department: 1
    }
  }
]);



// Task 37: Use $unwind to deconstruct the courses array

db.students.aggregate([
  { $unwind: "$enrolledCourses" }
]);



// Task 38: Use $limit to retrieve only the first 3 students

db.students.find().limit(3);



// Task 39: Use $skip to skip the first 2 students and get the rest

db.students.find().skip(2);



// Task 40: Use $lookup to join student data with courses

db.students.aggregate([
  {
    $lookup: {
      from: "courses",
      localField: "enrolledCourses",
      foreignField: "course_code",
      as: "courseDetails"
    }
  }
]);



// Task 41: Create a new collection for storing studentFeedback

db.studentFeedback.insertMany([
  {
    studentRollNumber: "CS1001",
    feedbackText: "Great experience with the courses!",
    date: new Date("2024-12-01")
  },
  {
    studentRollNumber: "CS1002",
    feedbackText: "Need more practical sessions.",
    date: new Date("2024-12-02")
  },
  {
    studentRollNumber: "CS1003",
    feedbackText: "The instructors are very supportive.",
    date: new Date("2024-12-03")
  }
]);



// Task 42: Query the studentFeedback collection to find feedback from a specific student

db.studentFeedback.find({ studentRollNumber: "CS1002" });



// Task 43: Use $set to update multiple fields at once

db.students.updateOne(
  { name: "Arjun" },
  {
    $set: {
      department: "Electronics Engineering",
      coursesEnrolled: ["EE101", "MATH202", "PHYS101"]
    }
  }
);



// Task 44: Create a custom index on the coursesEnrolled field

db.students.createIndex({ coursesEnrolled: 1 });



// Task 45: Perform a query on nested documents in the students collection

db.students.find({
  grades: {
    $elemMatch: { course: "CS101", grade: "A" }
  }
});

