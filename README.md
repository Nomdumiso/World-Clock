<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="src/style.css" />
    <script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.30.1/moment.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/moment-timezone/0.5.45/moment-timezone-with-data-1970-2030.min.js"></script>
    <title>World Clock - Nomdumiso Mtshilibe</title>
  </head>
  <body>
    <div class="container">
      <h1>World Clock ⏰</h1>

      <select id="city">
        <option value="">Select a city..</option>
        <option value="currentLocation">My current location</option>
        <option value="America/New_York">New York</option>
        <option value="Pacific/Fiji">Fiji</option>
        <option value="Australia/Melbourne">Melbourne</option>
      </select>
      <div id="cities">
        <div class="city" id="johannesburg">
          <div>
            <h2>Johannesburg</h2>
            <div class="date">August 15th 2022</div>
          </div>
          <div class="time">1:48:15 <small> AM </small></div>
        </div>
        <div class="city" id="london">
          <div>
            <h2>London</h2>
            <div class="date">August 15th 2022</div>
          </div>
          <div class="time">1:48:15 <small> AM </small></div>
        </div>
      </div>
    </div>
function updateTime() {
  let johannesburgElement = document.querySelector("#johannesburg");
  if (johannesburgElement) {
    let johannesburgDateElement = johannesburgElement.querySelector(".date");
    let johannesburgTimeElement = johannesburgElement.querySelector(".time");
    let johannesburgTime = moment().tz("Africa/Johannesburg");
    johannesburgDateElement.innerHTML = johannesburgTime.format("MMMM	Do YYYY");
    johannesburgTimeElement.innerHTML = johannesburgTime.format(
      "h:mm:ss [<small>]A[</small>]"
    );
  }
  let londonElement = document.querySelector("#london");
  if (londonElement) {
    let londonDateElement = londonElement.querySelector(".date");
    let londonTimeElement = londonElement.querySelector(".time");
    let londonTime = moment().tz("Europe/London");
    londonDateElement.innerHTML = londonTime.format("MMMM	Do YYYY");
    londonTimeElement.innerHTML = londonTime.format(
      "h:mm:ss [<small>]A[</small>]"
    );
  }
}

function updateCity(event) {
  let cityTimeZone = event.target.value;
  if (cityTimeZone === "currentLocation") {
    cityTimeZone = moment.tz.guess();
  }
  let cityName = cityTimeZone.replace("_", " ").split("/")[1];
  let cityTime = moment().tz(cityTimeZone);
  let citiesElement = document.querySelector("#cities");
  citiesElement.innerHTML = `
  <div class="city">
    <div>
      <h2>${cityName}</h2>
      <div class="date">${cityTime.format("MMMM	Do YYYY")}</div>
    </div>
    <div class="time">${cityTime.format("h:mm:ss")} <small>${cityTime.format(
    "A"
  )}</small></div>
  </div>
  `;
}
updateTime();
setInterval(updateTime, 1000);
let citiesSelectElement = document.querySelector("#city");
citiesSelectElement.addEventListener("change", updateCity);
