<script>
  import { onMount } from "svelte";
  let city = "New York";
  let searchQuery = "";
  let temperature = "22°C";
  let weatherIcon = "/images/rain.png";
  let humidity = "50%";
  let windSpeed = "15 km/h";

  const handleSearch = (event) => {
    event.preventDefault(); 
    if (searchQuery.trim()) {
      city = searchQuery;
      searchQuery = "";
    }
  };
</script>

<div class="card">
  <form class="search" on:submit={handleSearch}>
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
  
</style>
