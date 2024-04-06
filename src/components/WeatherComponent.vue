<template>
  <h2 v-if="loading">Loading...</h2>
  <h2 v-else>{{ weather }}</h2>
</template>

<script>
export default {
  name: 'WeatherComponent',
  data() {
    return {
      weather: '',
      loading: true
    };
  },
  mounted() {
        this.fetchWeather();
    },
    methods: {
        async fetchWeather() {
            try {
                const response = await fetch("https://api.weather.gov/points/42.7336,-84.5553");
                const data = await response.json();
                const forecastUrl = data.properties.forecast;

                const forecastResponse = await fetch(forecastUrl);
                const forecastData = await forecastResponse.json();

                // Extracting the current weather conditions
                const currentWeather = forecastData.properties.periods[0].detailedForecast;

                this.weather = currentWeather;
                this.loading = false;
            } catch (error) {
                console.error("Error fetching weather data:", error);
                this.weather = "Error fetching weather data";
                this.loading = false;
            }
        }
    }
}
</script>