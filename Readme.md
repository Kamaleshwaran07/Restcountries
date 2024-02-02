# Restcountries

## Fetch () API method

I stored the rest countries api url in a variable and fetched the data in a json format. 
After that I stored the latitude, longitude and weather api with latitude and longitude as input.

Then I created a div element and used template literal to display the required details.

```
let flagurl = country.flags.png;
        let lat = country.latlng[0];
        let lon = country.latlng[1];
        let countryCode = country.cca3;
        const weatherURL = `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=${apikey}`;

        let card = document.createElement("div");
        card.className = "card position-relative";
        card.style =
          "background-color: #FF3CAC;background-image: linear-gradient(225deg, #FF3CAC 0%, #784BA0 50%, #2B86C5 100%); text-align: center; align-items:center; box-shadow: 2px 2px 2px 2px purple; width: 24em; height: 35em; margin: 1em;";

        card.innerHTML = `
          <h4 class='card-header'>${country.name.common}</h4>
          <div style='justify-content: center'>
            <img src='${flagurl}' alt='country' style="height: 165px" width='300' />
          </div>
          <p>Capital: ${country.capital}</p>
          <p>Region: ${country.region}</p>
          <p class='fs-6'>Latitude: ${lat} Longitude: ${lon}</p>
          <p>Code: ${countryCode}</p>
          <div id='weather-${countryCode}'></div>
          <button class='bg-success btn position-absolute' id="weatherButton-${countryCode}" style="bottom:50px; text-align: center; width: 12em" onclick='displayWeather("${country.name.common}", "${country.capital}", ${lat}, ${lon}, "${countryCode}")'; type='button'>
            Click to see weather
          </button>
      
          
          <div id="weatherdisplay-${countryCode}" style="display: none;"></div>
        </div>`;

        cardBody.appendChild(card);
```

I added a onclick function to display the weather details and to hide the details when it is pressed again. I took the inspiration from the ToDo app building class.

```
function displayWeather(countryName, capital, lat, lon, code) {
  const weatherContainer = document.getElementById(`weather-${code}`);

  const weatherUrl = `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=290b1b2e0d95bbd3415fb67af86fd303`;

  fetch(weatherUrl)
    .then((response) => {
      if (!response.ok) {
        throw new Error(`Enna errornu paara ${response.status}`);
      }
      return response.json();
    })
    .then((weatherData) => {
      const climate = weatherData.weather[0].main;
      const temperature = weatherData.main.temp;
      weatherContainer.innerHTML = `<p style=""><span class="bg-primary rounded">Weather : ${climate}</span> <br/>
       <span class="bg-success rounded"> Temperature : ${temperature}</p></span> `;

      console.log(weatherContainer.style.display);
    })
}
```

To toggle the display : 

```
let weatherbutton = document.getElementById(
          `weatherButton-${countryCode}`
        );

        weatherbutton.addEventListener("click", () => {
          let weatherContainer = document.getElementById(
            `weather-${countryCode}`
          );
          if (weatherContainer.style.display == "flex") {
            weatherContainer.style.display = "none";
          } else {
            weatherContainer.style.display = "flex";
          }
        });
      
```