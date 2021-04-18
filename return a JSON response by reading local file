const http = require("http");
const url = require("url");
const fs = require("fs");

const PORT = 8080;

const server = http.createServer((req, res) => {
  // rejecting any other method than GET
  if (req.method !== "GET") {
    res.setHeader("Content-Type", "text/html");
    res.write("<p>please send a GET request</p>");
    res.end();
    return;
  }
  const { pathname } = url.parse(req.url, true); // parsing the url into an object and extracting the pathname
  // rejecting wrong pathnames
  if (pathname !== "/vegetables") {
    res.setHeader("Content-Type", "text/html");
    res.statusCode = 404;
    res.write("<p>page not found. the pathname should be '/vegetables'</p>");
    res.end();
    return;
  }

  fs.readFile("vegetables.json", (err, data) => {
    res.setHeader("Content-Type", "application/json");
    if (err) {
      err = JSON.stringify(err);
      res.write(err);
    } else {
      res.write(data);
    }
    res.end();
  });
});

server.listen(PORT, () => {
  console.log("server started at port " + PORT);
});
