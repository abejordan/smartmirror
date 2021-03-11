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
    axios.get("http://api.openweathermap.org/data/2.5/weather?q=Indianapolis&units=Imperial&appid=60c4d8818723401b5fad506c8226d9d2").then((current) => {
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
