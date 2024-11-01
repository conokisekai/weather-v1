<script>
  import { onMount } from "svelte";

  let city = "";
  let searchQuery = "";
  let temperature = "";
  let weatherIcon = "";
  let humidity = "";
  let windSpeed = "";
  const apiKey = "API_KEY";

  async function fetchWeather(city) {
    try {
      const response = await fetch(
        `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${apiKey}`
      );
      const data = await response.json();

      temperature = `${Math.round(data.main.temp)}°C`;
      weatherIcon = `http://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`;
      humidity = `${data.main.humidity}%`;
      windSpeed = `${data.wind.speed} km/h`;
    } catch (error) {
      console.error("Error fetching weather data:", error);
    }
  }

  const handleSearch = (event) => {
    event.preventDefault();
    if (searchQuery.trim()) {
      city = searchQuery;
      searchQuery = "";
      fetchWeather(city);
    }
  };

  onMount(() => {
    fetchWeather(city);
  });
</script>

<div class="card">
  <form class="search" onsubmit={handleSearch}>
    <input
      type="text"
      placeholder="Enter city name"
      spellcheck="false"
      bind:value={searchQuery}
    />
    <button type="submit"><img src="/images/search.png" alt="Search" /></button>
  </form>
  <div class="weather">
    <img src={weatherIcon} class="weather-icon" alt="Weather Icon" />
    <h1 class="temp">{temperature}</h1>
    <h2 class="city">{city}</h2>
    <div class="details">
      <div class="col">
        <img src="/images/humidity.png" alt="Humidity" />
        <p class="humidity">{humidity}</p>
        <p>Humidity</p>
      </div>
      <div class="col">
        <img src="/images/wind.png" alt="Wind Speed" />
        <p class="wind">{windSpeed}</p>
        <p>Wind Speed</p>
      </div>
    </div>
  </div>
</div>

<style>
  @import './app.css';
</style>