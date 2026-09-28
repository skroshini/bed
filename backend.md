Backend Development
1. Definition

Backend development is the part of a web application that runs on the server, behind the scenes. The user never sees it, but it makes the application work. It receives requests from the client, applies the business logic, talks to the database, and sends back a response.

If a website is a restaurant, the frontend is the dining area and menu. The backend is the kitchen: it takes the order, cooks it, and sends it out.

2. Main components of the backend
Server: a computer or program that listens for requests and sends responses (for example, Node.js with Express).
Application logic: the code that decides what to do with a request, such as validating a login, calculating a bill or processing an order.
Database: permanent storage for data such as users, products and orders (MySQL, MongoDB, PostgreSQL).
APIs: the interface through which the client and server communicate, usually with HTTP methods like GET, POST, PUT and DELETE.
Authentication and security: login, sessions or tokens, password hashing, and access control.
3. Web application architecture (three-tier)

A web application is divided into layers so that each part has one job. The diagram above shows the flow.
![Web Application Architecture]( web_application_architecture.svg )

Client (presentation tier): the browser or mobile app. It shows the user interface and sends HTTP requests (for example, a login form submission).

Web server: receives the incoming HTTP request, handles routing, and forwards it to the application. It can also serve static files such as HTML, CSS and images.

Application layer (logic tier): the core of the backend, written in Node.js/Express. It:

processes the request,
applies business rules and validation,
asks the database for data or saves data,
prepares the response.

Database (data tier): stores data permanently. It runs the query sent by the application layer and returns the result.

4. Working (request–response cycle) 
   
The user performs an action in the browser, for example clicking "Login".
The client sends an HTTP request to the web server.
The web server forwards it to the application layer.
The application layer validates the input and sends a query to the database.
The database returns the matching data.
The application layer builds the response (HTML or JSON).
The response travels back through the web server to the client, and the browser displays it.
6. Advantages of layered architecture
Separation of concerns: each layer has one clear responsibility.
Scalability: each layer can be scaled independently.
Security: the client never accesses the database directly.
Maintainability: one layer can be changed without rewriting the others.
Reusability: the same backend can serve a website and a mobile app.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

2Q)Write an express dot JS application to handle GET POST PUT and DELETE request for student information,(8marks )
// server.js
// Express application to handle GET, POST, PUT and DELETE for student information

const express = require('express');
const app = express();

// Middleware: lets Express read JSON data sent in the request body
app.use(express.json());

// In-memory data (acts like a small database)
let students = [
  { id: 1, name: 'Ravi', branch: 'CSE', year: 2 },
  { id: 2, name: 'Sita', branch: 'ECE', year: 2 }
];

// GET /students -> read all students
app.get('/students', (req, res) => {
  res.status(200).json(students);
});

// GET /students/:id -> read one student
app.get('/students/:id', (req, res) => {
  const student = students.find(s => s.id === parseInt(req.params.id));
  if (!student) {
    return res.status(404).json({ message: 'Student not found' });
  }
  res.status(200).json(student);
});

// POST /students -> create a new student
app.post('/students', (req, res) => {
  const { name, branch, year } = req.body;
  if (!name || !branch || !year) {
    return res.status(400).json({ message: 'name, branch and year are required' });
  }
  const newStudent = {
    id: students.length ? students[students.length - 1].id + 1 : 1,
    name,
    branch,
    year
  };
  students.push(newStudent);
  res.status(201).json(newStudent);
});

// PUT /students/:id -> update an existing student
app.put('/students/:id', (req, res) => {
  const student = students.find(s => s.id === parseInt(req.params.id));
  if (!student) {
    return res.status(404).json({ message: 'Student not found' });
  }
  const { name, branch, year } = req.body;
  if (name) student.name = name;
  if (branch) student.branch = branch;
  if (year) student.year = year;
  res.status(200).json(student);
});

// DELETE /students/:id -> remove a student
app.delete('/students/:id', (req, res) => {
  const index = students.findIndex(s => s.id === parseInt(req.params.id));
  if (index === -1) {
    return res.status(404).json({ message: 'Student not found' });
  }
  const removed = students.splice(index, 1);
  res.status(200).json({ message: 'Student deleted', student: removed[0] });
});

// Start the server
const PORT = 3000;
app.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

3Q))**Compare front end and back end development based on architecture ,technologies  Responsibilities ,scalability, and security(8m)**


**Front End vs Back End Development
Introduction**

Front end development builds the part of a web application that the user sees and interacts with (the client side). Back end development builds the part that runs on the server, handling logic, data and security (the server side). Both must work together for a complete application.

**Comparison table**:-
![Screenshot%202026-09-28%20214726](Screenshot%202026-09-28%20214726.png)
