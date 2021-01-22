<template>
  <div id="app">
    <Weather
      v-bind:temp="temp"
      v-on:change-city="updateCity"
      v-bind:selectedCity="selectedCity"
      v-bind:weather="weather"
      v-bind:image="image"
      v-bind:tempcolor="tempcolor"
    />
  </div>
</template>

<script>
import Weather from "./components/Weather.vue";

export default {
  name: "App",
  data: () => ({
    //!Please get an API key for openweathermap and paste it below
    apiKey: "",
    temp: 0,
    selectedCity: "Tokyo",
    weather: "loading...",
    image: "",
    tempcolor: "",
  }),
  components: {
    Weather,
  },
  methods: {
    fetchWeatherData: async function(city) {
      const callUrl = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${this.apiKey}`;
      const fetchedData = await fetch(callUrl);
      const jsoned = await fetchedData.json();
      return this.updatedWeatherData(jsoned);
    },
    updatedWeatherData: function(json) {
      this.temp = json.main.temp;
      this.weather = this.fixWeatherString(json.weather[0].description);
      this.checkWeather(json.weather[0].main);
    },
    updateCity: function(city) {
      this.selectedCity = city;
      this.fetchWeatherData(this.selectedCity);
    },
    checkWeather: function(weather) {
      console.log(weather);
      if (weather === "Mist" || weather === "Rain" || weather === "Stormy") {
        this.image = "rainy";
        this.tempcolor = "rainColor";
      } else if (weather === "Clouds") {
        this.image = "cloudy";
        this.tempcolor = "cloudColor";
      } else if (weather === "Clear") {
        this.tempcolor = "sunColor";
        this.image = "sunny";
      } else {
        this.tempcolor = "snowColor";
        this.image = "snowy";
      }
    },
    fixWeatherString: function(string) {
      const result = string.split(" ");
      return result
        .map((word) => {
          return word.charAt(0).toUpperCase() + word.slice(1);
        })
        .join(" ");
    },
  },
  created: function() {
    this.fetchWeatherData(this.selectedCity);
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
.rainColor {
  background: rgba(149, 175, 232, 0.317);
}

.rainy {
  background-image: url("https://images.unsplash.com/photo-1534274988757-a28bf1a57c17?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1575&q=80");
}

.cloudy {
  background-image: url("https://images.unsplash.com/photo-1592601250984-da0dc45e25f7?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1534&q=80");
}

.cloudColor {
  background: rgba(152, 147, 147, 0.372);
}

.sunny {
  background: url("https://images.unsplash.com/photo-1587993202407-88b4156fe89f?ixlib=rb-1.2.1&ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&auto=format&fit=crop&w=1952&q=80");
}

.sunColor {
  background: rgba(181, 171, 115, 0.303);
}

.snowy {
  background: url("https://images.unsplash.com/photo-1548777123-e216912df7d8?ixlib=rb-1.2.1&ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&auto=format&fit=crop&w=1575&q=80");
}

.snowColor {
  background: rgba(198, 198, 210, 0.529);
}
</style>
