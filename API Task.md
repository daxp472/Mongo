### By course name

```javascript

import express from 'express';
import { MongoClient } from 'mongodb';

const app = express();
const port = 3000;

const uri = "mongodb://localhost:27017/";
const dbName = "codinggita";

app.use(express.json());

let db, courses;

async function initializeDatabase() {
    try {
        const client = await MongoClient.connect(uri, { useUnifiedTopology: true });
        console.log("Connected to MongoDB");

        db = client.db(dbName);
        courses = db.collection("courses");

        app.listen(port, () => {
            console.log(`Server running at http://localhost:${port}`);
        });
    } catch (err) {
        console.error("Error connecting to MongoDB:", err);
        process.exit(1);
    }
}

initializeDatabase();



app.get('/courses', async (req, res) => {
    try {
        const allCourses = await courses.find().toArray();
        res.status(200).json(allCourses);
    } catch (err) {
        res.status(500).send("Error fetching courses: " + err.message);
    }
});


app.post('/courses', async (req, res) => {
    try {
        const newCourse = req.body;
        const result = await courses.insertOne(newCourse);
        res.status(201).send(`Course added with ID: ${result.insertedId}`);
    } catch (err) {
        res.status(500).send("Error adding course: " + err.message);
    }
});


app.put('/courses/:courseCode', async (req, res) => {
    try {
        const courseCode = req.params.courseCode;
        const updatedCourse = req.body;
        const result = await courses.replaceOne({ courseCode }, updatedCourse);
        res.status(200).send(`${result.modifiedCount} document(s) updated`);
    } catch (err) {
        res.status(500).send("Error updating course: " + err.message);
    }
});


app.patch('/courses/v1/:courseCode', async (req, res) => {
    try {
        const courseCode = req.params.courseCode;
        const updates = req.body;
        const result = await courses.updateOne({ courseCode }, { $set: updates });
        res.status(200).send(`${result.modifiedCount} document(s) updated`);
    } catch (err) {
        res.status(500).send("Error partially updating course: " + err.message);
    }
});


app.delete('/courses/ByCode/:courseCode', async (req, res) => {
    try {
        const courseCode = req.params.courseCode;
        const result = await courses.deleteOne({ courseCode });
        if (result.deletedCount > 0) {
            res.status(200).send(`${result.deletedCount} document(s) deleted`);
        } else {
            res.status(404).send("No course found with the specified course code");
        }
    } catch (err) {
        res.status(500).send("Error deleting course by code: " + err.message);
    }
});

```


### By course code

```javascript


import express from 'express';
import { MongoClient, ObjectId } from 'mongodb'; // Correct import for ObjectId

const app = express();
const port = 4000;

const uri = "mongodb://localhost:27017/";
const dbName = "CodingGitaStudents";

app.use(express.json());

let db, courses;

async function initializeDatabase() {
    try {
        const client = await MongoClient.connect(uri, { useUnifiedTopology: true });
        console.log("Connected to MongoDB");

        db = client.db(dbName);
        courses = db.collection("courses");

        app.listen(port, () => {
            console.log(`Server running at http://localhost:${port}`);
        });
    } catch (err) {
        console.error("Error connecting to MongoDB:", err);
        process.exit(1);
    }
}

initializeDatabase();

app.get('/courses', async (req, res) => {
    try {
        const allCourses = await courses.find().toArray();
        res.status(200).json(allCourses);
    } catch (err) {
        res.status(500).send("Error fetching courses: " + err.message);
    }
});

app.post('/courses', async (req, res) => {
    try {
        const newCourse = req.body;
        const result = await courses.insertOne(newCourse);
        res.status(201).send(`Course added with ID: ${result.insertedId}`);
    } catch (err) {
        res.status(500).send("Error adding course: " + err.message);
    }
});

app.put('/courses/:id', async (req, res) => {
    try {
        const courseId = req.params.id;
        const updatedCourse = req.body;
        const result = await courses.replaceOne({ _id: new ObjectId(courseId) }, updatedCourse); // Corrected here
        res.status(200).send(`${result.modifiedCount} document(s) updated`);
    } catch (err) {
        res.status(500).send("Error updating course: " + err.message);
    }
});

app.patch('/courses/v1/:id', async (req, res) => {
    try {
        const courseId = req.params.id;
        const updates = req.body;
        const result = await courses.updateOne({ _id: new ObjectId(courseId) }, { $set: updates }); // Corrected here
        res.status(200).send(`${result.modifiedCount} document(s) updated`);
    } catch (err) {
        res.status(500).send("Error partially updating course: " + err.message);
    }
});

app.delete('/courses/ById/:id', async (req, res) => {
    try {
        const courseId = req.params.id;
        const result = await courses.deleteOne({ _id: new ObjectId(courseId) });
        if (result.deletedCount > 0) {
            res.status(200).send(`${result.deletedCount} document(s) deleted`);
        } else {
            res.status(404).send("No course found with the specified ID");
        }
    } catch (err) {
        res.status(500).send("Error deleting course by ID: " + err.message);
    }
});


```


Course API Documentation
========================

Overview
--------

This API provides a simple interface for managing courses. It supports GET, POST, PUT, PATCH, and DELETE requests.

Endpoints
---------

### GET /courses

*   Retrieves a list of all courses.

### POST /courses

*   Creates a new course.

### PUT /courses/:id

*   Updates a course by ID.

### PATCH /courses/v1/:id

*   Partially updates a course by ID.

### DELETE /courses/ById/:id

*   Deletes a course by ID.

### GET /courses

*   Retrieves a list of all courses.

### POST /courses

*   Creates a new course.

### PUT /courses/:courseCode

*   Updates a course by course code.

### PATCH /courses/v1/:courseCode

*   Partially updates a course by course code.

### DELETE /courses/ByCode/:courseCode

*   Deletes a course by course code.

API Documentation Link
----------------------

https://documenter.getpostman.com/view/39216571/2sAYJAexrg
