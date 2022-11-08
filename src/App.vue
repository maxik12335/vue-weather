<template>
  <div>
    <div class="container">
      <list-cities 
        :listCitiesRu="listCitiesRu"
        @clickCity="clickCity"
      />

      <card-city 
        v-if="cityData.showCard"
        :cityData="cityData"
      />
    </div>
  </div>
</template>

<script>
import ListCities from "@/components/ListCities.vue"
import CardCity from "@/components/CardCity.vue"
export default {
  components: {
    ListCities,
    CardCity
  },
  data() {
    return {
      weatherData: [
        {cityName: {en: "Nizhny Novgorod", ru: "Нижний Новгород"}},
        {cityName: {en: "Alexin", ru: "Алексин"}},
        {cityName: {en: "Cheboksary", ru: "Чебоксары"}},
        {cityName: {en: "Tula", ru: "Тула"}},
        {cityName: {en: "Moscow", ru: "Москва"}},
      ],

      cityData: {
        showCard: false,
        name: "",
        temperature: "",
      }
    };
  },

  mounted() {
    this.setCoordinatesCities()
  },

  computed: {
    listCitiesRu() {
      const arrayCitiesNames = []
      
      this.weatherData.forEach(item => {
        arrayCitiesNames.push(item.cityName.ru)
      })

      return arrayCitiesNames
    },
  },

  methods: {
    setCoordinatesCities() {
      this.weatherData.forEach(city => {
        this.getCoordinatesByFetchCityName(city)
      })
    },

    getCoordinatesByFetchCityName(cityElement) {
      fetch(`http://api.openweathermap.org/geo/1.0/direct?q=${cityElement.cityName.en}&appid=3cbbcc71f8eea3440fd826fe5f9d0adb`)
      .then(response => response.json())
      .then(response => {
        cityElement.lat = response[0].lat
        cityElement.lon = response[0].lon
      })
    },

    getTemperatureByCoordinatesCity(city) {
      let foundCity = this.weatherData.filter(cityItem => cityItem.cityName.ru === city)[0]
      let {lat, lon} = foundCity

      fetch(`http://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=3cbbcc71f8eea3440fd826fe5f9d0adb`)
        .then(response => response.json())
        .then(response => {
          foundCity.temperature = response.main.temp
          this.cityData = {
            showCard: true,
            name: foundCity.cityName.ru,
            temperature: Math.round(foundCity.temperature - 273.15)
          }
        })
    },

    // переименовать clickCity и foundCity придумать что-то с cityData
    clickCity(cityName) {
      this.getTemperatureByCoordinatesCity(cityName)
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

ul {
  list-style-type: none;
}

.container {
  margin: 50px auto;
  width: 1200px;
}
</style>
