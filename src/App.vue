<template>
  <div>
    <div class="container">
      <h1 class="main-title">ПОГОДА</h1>

      <list-cities 
        :listCitiesData="listCitiesData"
        @updateDataSelectedCity="updateDataSelectedCity"
        @openCitiesMenu="openCitiesMenu"
      />

      <card-city 
        v-if="dataSelectedCity.showCard"
        :dataSelectedCity="dataSelectedCity"
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
        {cityName: {en: "Nizhny Novgorod", ru: "Нижний Новгород"}, latitude: 56.32,longitude: 44.00},
        {cityName: {en: "Alexin", ru: "Алексин"}, latitude: 54.30,longitude: 37.04},
        {cityName: {en: "Cheboksary", ru: "Чебоксары"}, latitude: 56.13,longitude: 47.25},
        {cityName: {en: "Tula", ru: "Тула"}, latitude: 54.19,longitude: 37.61},
        {cityName: {en: "Moscow", ru: "Москва"}, latitude: 55.45,longitude: 37.36},
      ],

      dataSelectedCity: {
        showCard: false,
        name: "",
        temperature: "",
      },

      listCitiesData: {
        menuListCities: Array,
        showListCitiesElements: {
          citiesButton: true,
          citiesList: true
        }
      }
    };
  },

  mounted() {
    this.setTemperatureCities()
    this.setMenuListCities()
    this.setStartShowListCitiesElements()
  },

  methods: {
    setMenuListCities() {
      const arrayCitiesNames = []
      
      this.weatherData.forEach(item => {
        arrayCitiesNames.push(item.cityName.ru)
      })

      this.listCitiesData.menuListCities = arrayCitiesNames
    },

    setTemperatureCities() {
      this.weatherData.forEach(city => {
        this.getTemperatureCity(city)
      })
    },

    getTemperatureCity(city) {
      let {latitude, longitude} = city

      fetch(`https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&hourly=temperature_2m`)
        .then(response => response.json())
        .then(response => {
          city.temperature = response.hourly.temperature_2m[new Date().getHours() - 1]
        })
    },

    updateDataSelectedCity(city) {
      if(window.innerWidth < 768 ) {
        this.listCitiesData.showListCitiesElements = {
          citiesButton: true, 
          citiesList: false
        }
      }

      this.dataSelectedCity.showCard = true
      this.dataSelectedCity.name = this.weatherData.filter(item => item.cityName.ru === city)[0].cityName.ru
      this.dataSelectedCity.temperature = this.weatherData.filter(item => item.cityName.ru === city)[0].temperature
    },

    openCitiesMenu() {
      this.listCitiesData.showListCitiesElements = {
        citiesButton: false, 
        citiesList: true
      }

      this.dataSelectedCity.showCard = false
    },

    setStartShowListCitiesElements() {
      window.innerWidth < 768 ? 
        this.listCitiesData.showListCitiesElements = {citiesButton: true, citiesList: false} : 
        this.listCitiesData.showListCitiesElements = {citiesButton: false, citiesList: true}
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

body {
  font-family: Arial, Helvetica, sans-serif;
  background: #0e0e0e;
  color: white;
}

ul {
  list-style-type: none;
}

.container {
  margin: 20px auto;
  width: 1200px;
}

.main-title {
  text-align: center;
  margin-bottom: 30px;
}

@media(max-width: 1230px) {
  .container {
    width: 768px;
  }
}

@media(max-width: 800px) {
  .container {
    width: 300px;
  }
}
</style>
