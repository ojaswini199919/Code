const http = require("http");
const url = require("url");

const PORT = 8080;

const calculateCircleArea = ({ metric, radius }) => {
  if (metric === "area") {
    if (isNaN(radius) || radius === "") return "<p>radius must be a number</p>";
    return `<p>area of the circle is ${(Math.PI * radius * radius).toFixed(
      2
    )}</p>`;
  } else {
    return "<p>for a cricle object you should have <i><b>metric=area</b></i> in the url</p>";
  }
};

const calculateSphereVolume = ({ metric, radius }) => {
  switch (metric) {
    case "volume":
      if (isNaN(radius) || radius === "")
        return "<p>radius must be a number</p>";
      return `<p>volume of the sphere is ${(
        (4 / 3) *
        Math.PI *
        Math.pow(radius, 3)
      ).toFixed(2)}</p>`;
    case "surfaceArea":
      if (isNaN(radius) || radius === "")
        return "<p>radius must be a number</p>";
      return `<p>surfaceArea of the shphere is ${(
        4 *
        Math.PI *
        Math.pow(radius, 2)
      ).toFixed(2)}</p>`;
    default:
      return "<p>for a cricle object you should have <i><b>metric=volume or metric=surfaceArea</b></i> in the url</p>";
  }
};

const server = http.createServer((req, res) => {
  res.setHeader("Content-Type", "text/html");
  // check the method of the request
  if (req.method === "GET") {
    // parse the query parameters
    const parsedUrl = url.parse(req.url, true);
    if (parsedUrl.pathname === "/metrics") {
      const { object } = parsedUrl.query;
      switch (object) {
        case "circle":
          res.write(calculateCircleArea(parsedUrl.query));
          break;
        case "sphere":
          res.write(calculateSphereVolume(parsedUrl.query));
          break;
        default:
          res.write(
            "<p>use <b><i>circle</i></b> or <b><i>sphere</i></b> as object value</p>"
          );
      }
    } else {
      res.write(
        "<p>url not valid. please use <b><i>metrics</i></b> as pathname"
      );
    }
  } else {
    res.write("<p>please send GET request only</p>");
  }
  res.end();
});

server.listen(PORT, () => {
  console.log("server started at port " + PORT);
});
