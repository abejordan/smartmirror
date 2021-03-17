<template>
  <div class=" col-span-2">
    <div v-if="weather != null" class="flex flex-row">
      <div>
        <img
          class="h-16 mr-4"
          v-bind:src="getImgUrl(weather.current.weather[0].icon + '.svg')"
        />
      </div>
      <div>
        <h2 class="dark:text-white text-4xl">
          {{ weather.current.temp | round }}&#8457;
        </h2>
        <h2 class="dark:text-white text-2xl">
          {{ weather.current.weather[0].main }}
        </h2>
      </div>
    </div>
    <div v-if="weather != null" class="flex pt-6">
      <div
        class="px-4 flex flex-col items-center"
        v-for="daily in weather.daily"
        :key="daily.dt"
      >
        <p class="dark:text-white">{{ daily.dt | toDay }}</p>
        <div class="h-16 flex">
          <img class="w-14" :src="getImgUrl(daily.weather[0].icon + '.svg')" />
        </div>
        <div class="pt-2">
          <p class="dark:text-white">{{ daily.temp.max | round }}&#8457;</p>
          <p class="dark:text-white">{{ daily.weather[0].main }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      weather: null,
      forecast: null,
    };
  },
  created() {
    let api_key = process.env.VUE_APP_WEATHER_API_KEY;
    axios
      .get(
        "https://api.openweathermap.org/data/2.5/onecall?lat=39.791&lon=-86.148003&exclude=hourly&units=imperial&appid=" +
          api_key +
          ""
      )
      .then((current) => {
        this.weather = current.data;
        console.log(current.data);
      });
  },
  methods: {
    getImgUrl(pic) {
      return require("../assets/images/" + pic);
    },
  },
  filters: {
    round: function(value) {
      if (!value) {
        value = 0;
      }
      value = Math.round(value);
      return value;
    },
    toDay: function(value) {
      const days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      const now = new Date(value * 1000);
      let day = days[now.getDay()];
      return day;
    },
  },
};
</script>
