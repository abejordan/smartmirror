<template>
  <div class=" flex justify-end items-start">
    <div>
      <p class="dark:text-white text-lg">{{dayName}}, {{monthName}} {{date}}, {{year}}</p>
    <p class=" text-6xl font-bold dark:text-white">{{hours}}:{{minutes}} {{hourtime}}</p>
    </div>
  </div>
</template>

<script>
import { SECOND, HOUR, getHourTime, getZeroPad } from './filters/time';
export default {
    data() {
    return {
      monthName:'',
      dayName:'',
      year:'',
      date:'',
      hours: 0,
      minutes: 0,
      seconds: 0,
      hourtime: '',
    };
  },
mounted(){
this.$options.timer = window.setTimeout(this.updateDateTime, SECOND);
},
methods:{
  updateDateTime(){
    const now = new Date()
     const months = [
  'January',
  'February',
  'March',
  'April',
  'May',
  'June',
  'July',
  'August',
  'September',
  'October',
  'November',
  'December'
]
const days = [
  'Sunday',
  'Monday',
  'Tuesday',
  'Wednesday',
  'Thursday',
  'Friday',
  'Saturday'
]
      this.monthName = months[now.getMonth()];
      this.dayName = days[now.getDay()];
      this.year = now.getFullYear();
      this.date = now.getDate();
      this.hours = now.getHours();
      this.minutes = getZeroPad(now.getMinutes());
      this.seconds = getZeroPad(now.getSeconds());
      this.hourtime = getHourTime(this.hours);
      this.hours = this.hours % HOUR || HOUR;
      this.$options.timer = window.setTimeout(this.updateDateTime, SECOND);
  }
}
}
</script>

<style>

</style>