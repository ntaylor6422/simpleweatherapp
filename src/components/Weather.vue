<template>
  <div class="weather weather-image" v-bind:class="image">
    <section class="allContent">
      <Search v-on="$listeners" v-bind:selectedCity="selectedCity" />
      <div class="weatherDetails" v-bind:class="tempcolor">
        <h2 id="weatherCondition">{{ weather }}</h2>
        <h2 id="temperature">{{ Math.floor(temp) }}°C</h2>
      </div>
    </section>
  </div>
</template>

<script>
import Search from "./Search.vue";

export default {
  name: "Weather",
  components: {
    Search,
  },
  props: {
    temp: Number,
    selectedCity: String,
    weather: String,
    image: String,
    tempcolor: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.weather {
  display: grid;
  grid-template-rows: 3fr 2fr 5fr 3fr;
  grid-template-columns: 2fr 5fr 5fr 2fr;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100vw;
}

.allContent {
  background-color: rgba(185, 215, 225, 0.564);
  border-radius: 2rem;
  grid-column: 2 / 4;
  grid-row: 2 / 4;
  height: 100%;
  width: 100%;
  display: grid;
  grid-template-rows: 2fr 5fr 3fr;
  grid-template-columns: 2fr 5fr 5fr 2fr;
  box-shadow: 2px 2px 2px 2px rgba(91, 90, 90, 0.461);
}

.weather-image {
  background-repeat: no-repeat;
  background-size: cover;
}

.weatherDetails {
  grid-row: 2 / 4;
  grid-column: 1 / 5;
  display: grid;
  grid-template-rows: 3fr 7fr;
  border-radius: 2rem;
}

#weatherCondition {
  grid-row: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 30px;
}

#temperature {
  grid-row: 2;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 80px;
}
</style>
