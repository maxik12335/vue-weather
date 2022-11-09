<template>
  <div>
    <button
      class="cities-button"
      v-if="showCitiesButton"
      @click="$emit('openCitiesMenu')"
    >
      Выбери город
    </button>

    <ul 
      class="cities-list"
      v-if="showCitiesList"
    >
      <li
        v-for="city in menuListCities" 
        :key="city"
        class="cities-list-item"
        @click="$emit('updateDataSelectedCity', city)"
      >
        {{ city }}
      </li>
    </ul>
  </div>  
</template>

<script>
export default {
  props: {
    listCitiesData: {
      type: Object,
      required: true
    }
  },

  computed: {
    menuListCities() {
      return this.listCitiesData.menuListCities
    },

    showCitiesButton() {
      return this.listCitiesData.showListCitiesElements.citiesButton
    },

    showCitiesList() {
      return this.listCitiesData.showListCitiesElements.citiesList
    },
  }
}
</script>

<style>
.cities-list {
  display: flex;
  justify-content: center;
}

.cities-list-item {
  margin: 0 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  border: 1px solid;
  border-radius: 5px;
  padding: 10px 20px;
  width: 200px;
  cursor: pointer;
}

.cities-list-item:hover {
  background-color: #e7e4e0;
  color: #4a4a4a;
}

.cities-button {
  width: 100%;
  height: 50px;
  background-color: transparent;
  border: 1px solid white;
  color: white;
  border-radius: 5px;
}

@media(max-width: 800px) {
  .cities-list {
    flex-direction: column;
  }

  .cities-list-item {
    width: 100%;
    margin: 0;
  }

  .cities-list-item:not(:last-child) {
    margin-bottom: 20px;
  }
}
</style>