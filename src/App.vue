<template>
  <div id="app">
    <div class="grid grid-cols-3 gap-4 p-12">
    <Weather />
    <Time />
    <News />
    </div>
  </div>
</template>
<script>
import News from './components/News'
import Weather from './components/Weather'
import Time from './components/Time'
export default {
  name: 'App',
  components: {
    Weather,
    Time,
    News
  }
}
</script>

<style>

</style>
