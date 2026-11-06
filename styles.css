let form = document.querySelector("form");
let cityInput = document.querySelector("#city-input");
let results = document.querySelector("#results");
let locationBtn = document.querySelector("#location-btn");
let clearBtn = document.querySelector("#clear-btn");

form.addEventListener("submit", async (event) => {
  event.preventDefault();

  let city = cityInput.value;
  let url = `https://geocoding-api.open-meteo.com/v1/search?name=${city}`;

  let response = await fetch(url);
  let data = await response.json();

  let latitude = data.results[0].latitude;
  let longitude = data.results[0].longitude;

  let cityName = data.results[0].name;

let country = data.results[0].country;



let weatherUrl =
  `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&current=temperature_2m,wind_speed_10m,weather_code,relative_humidity_2m&daily=temperature_2m_max,temperature_2m_min`;
  
  

let weatherResponse = await fetch(weatherUrl);

let weatherData = await weatherResponse.json();


let temperature = weatherData.current.temperature_2m;

let windSpeed = weatherData.current.wind_speed_10m;

let weatherCode = weatherData.current.weather_code;

let updateTime = weatherData.current.time;
let humidity = weatherData.current.relative_humidity_2m;


let weatherCondition = "";

if (weatherCode === 0) {
  weatherCondition = "☀️ Clear Sky";
}

if (weatherCode === 1) {
  weatherCondition = "🌤️ Mainly Clear";
}

if (weatherCode === 2) {
  weatherCondition = "⛅ Partly Cloudy";
}

if (weatherCode === 3) {
  weatherCondition = "☁️ Overcast";
}


let forecastHTML = "";

for (let i = 0; i < weatherData.daily.time.length; i++) {

  let date = new Date(weatherData.daily.time[i]);

  let day = date.toLocaleDateString("en-US", {
    weekday: "long"
  });

  forecastHTML += `
    <div class="forecast-card">
      <p>${day}</p>
      <p>🔺 High: ${weatherData.daily.temperature_2m_max[i]}°C</p>
      <p>🔻 Low: ${weatherData.daily.temperature_2m_min[i]}°C</p>
    </div>
  `;
}

results.innerHTML = `
  <h2>${cityName}, ${country}</h2>
  <p>${weatherCondition}</p>
  <p>🌡️ Temperature: ${temperature}°C</p>
  <p>💨 Wind Speed: ${windSpeed} km/h</p>
  <p>💧 Humidity: ${humidity}%</p>
  <p>🕒 Updated: ${updateTime}</p>

  <hr>

  <h3>7-Day Forecast</h3>

  ${forecastHTML}
`;

});

locationBtn.addEventListener("click", () => {
  navigator.geolocation.getCurrentPosition(getWeatherByLocation);
});

async function getWeatherByLocation(position) {
  let latitude = position.coords.latitude;
  let longitude = position.coords.longitude;

  let weatherUrl =
    `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&current=temperature_2m,wind_speed_10m,weather_code,relative_humidity_2m&daily=temperature_2m_max,temperature_2m_min`;

  let weatherResponse = await fetch(weatherUrl);

  let weatherData = await weatherResponse.json();

  console.log(weatherData);
}

clearBtn.addEventListener("click", () => {
  cityInput.value = "";
  results.innerHTML = "";
});
