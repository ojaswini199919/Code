const http = require("http");
const url = require("url");

const PORT = 8080;

const calculateAge = (year, month, date) => {
  let dateObj = new Date(),
    age;
  const [curYear, curMonth, curDate] = [
    dateObj.getFullYear(),
    dateObj.getMonth() + 1,
    dateObj.getDate(),
  ];
  age = curYear - year;
  if (curMonth < month) age--;
  else if (curMonth == month && curDate < date) age--;
  return age;
};

// creating an instance of http.server class
const server = http.createServer((req, res) => {
  if (req.method === "GET") {
    res.setHeader("Content-Type", "text/html");
    const parsedUrl = url.parse(req.url, true);
    if (parsedUrl.pathname !== "/age") {
      res.statusCode = 404;
      res.write(`<p>Page not found... The pathname should be '/age'</p>`);
      res.end();
      return;
    }
    let { year, month, date, name } = parsedUrl.query; //extracting the query params
    year = parseInt(year);
    month = parseInt(month);
    date = parseInt(date);
    if (isNaN(year) || isNaN(month) || isNaN(date) || name === "") {
      // rejecting wrong param vales
      res.write("<p>query paramameters are not valid</p>");
    } else {
      let age = calculateAge(year, month, date);
      res.write(`<p>Hello ${name}</p>`);
      res.write(`<p>You are ${age} years old.</p>`);
    }
  } else {
    res.write("please send a GET request!");
  }
  res.end();
});

server.listen(`${PORT}`, () => {
  console.log(`server running at ${PORT}`);
});
