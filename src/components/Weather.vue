<template>
  <div v-if="currentWeather != null" class=" border col-span-2">
    <div class="flex flex-col ">
    <img class=" w-20" v-bind:src="'http://openweathermap.org/img/w/'+currentWeather.weather[0].icon+'.png'">
    <h2 class="dark:text-white text-2xl">{{currentWeather.main.temp | round }}&#8457;</h2>
    <h2 class="dark:text-white text-lg">{{currentWeather.weather[0].main}}</h2>
    <p class="dark:text-white text-lg">{{currentWeather.weather[0].description}}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      currentWeather: null,
      forecast: null
    };
  },
  created() {
    let api_key = process.env.VUE_APP_WEATHER_API_KEY
    axios.get("http://api.openweathermap.org/data/2.5/weather?q=Indianapolis&units=Imperial&appid="+api_key+"").then((current) => {
      this.currentWeather = current.data;
      console.log(current);
    });
  },
  filters: {
  round: function (value) {
  if(!value) {
    value = 0;
  }
  value = Math.round(value);
  return value;
  }
}
};
</script>

<style></style>
