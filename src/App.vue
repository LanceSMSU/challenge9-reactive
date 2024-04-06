<template>
  <h1>This is my weather Vue app to display weather information for East Lansing</h1>
  <WeatherComponent/>
</template>

<script>
import WeatherComponent from './components/WeatherComponent.vue'

export default {
  name: 'App',
  components: {
    WeatherComponent
  }
}
</script>
