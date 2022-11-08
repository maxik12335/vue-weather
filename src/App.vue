<template>
  <div>
    <button @click="getTemperatureByCoordinatesCite('Alexin')">Alexin</button>
  </div>
</template>

<script>
// import CardCity from './components/CardCity.vue';
export default {
  // components: { CardCity },
  data() {
    return {
      weatherData: [
        {cityName: "Nizhny Novgorod"},
        {cityName: "Alexin"},
      ],
    };
  },

  mounted() {
    this.setCoordinatesCities()    
  },

  methods: {
    setCoordinatesCities() {
      this.weatherData.forEach(city => {
        this.getCoordinatesByFetchCityName(city)
      })
    },

    getCoordinatesByFetchCityName(cityElement) {
      fetch(`http://api.openweathermap.org/geo/1.0/direct?q=${cityElement.cityName}&appid=3cbbcc71f8eea3440fd826fe5f9d0adb`)
      .then(response => response.json())
      .then(response => {
        cityElement.lat = response[0].lat
        cityElement.lon = response[0].lon
      })
    },

    getTemperatureByCoordinatesCite(city) {
      let foundCity = this.weatherData.filter(cityItem => cityItem.cityName === city)[0]
      let {lat, lon} = foundCity

      fetch(`http://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=3cbbcc71f8eea3440fd826fe5f9d0adb`)
        .then(response => response.json())
        .then(response => {
          foundCity.temperature = response.main.temp
        })
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
