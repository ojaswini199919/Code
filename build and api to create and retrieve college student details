const express = require("express");
const fs = require("fs");

const PORT = 3000;

const app = express(); // creating an instance of the express class

app.use(express.json()); // parsing the json object to javascript object when any json is sent in request body

app.get("/student/getDetails", (req, res, next) => {
  fs.readFile("studentDetails.json", "utf8", (error, data) => {
    if (error) res.json(error);
    else {
      data = JSON.parse(data);
      res.send(data);
    }
  });
});

app.post("/student/add", (req, res, next) => {
  const studentDetails = JSON.stringify(req.body);
  fs.writeFile("studentDetails.json", studentDetails, (error) => {
    if (error) res.json(error);
    else res.json({ result: "success" });
  });
});

// when user enters some invalid url this middleware gets executed
app.use((req, res, next) => {
  res.setHeader("Content-Type", "text/html");
  res.status(404).send(`<h1>something went wrong.</h1>`);
});

// this is the default error handler
app.use((err, req, res, next) => {
  res.json("some error occurred while creating the file");
});

app.listen(PORT, () => {
  console.log(`server started at port ${PORT}`);
});
