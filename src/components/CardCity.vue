<template>
  <div>
    <div class="card-city">
      <h2 class="card-city__name">{{ cityData.name }}</h2>
      <p class="card-city__temperature">Темпартура: {{ cityData.temperature }} 	&#176;С</p>
    </div>
  </div>  
</template>

<script>
export default {
  props: {
    cityData: {
      type: Object,
      required: true,
    }
  }
}
</script>

<style>
.card-city {
  width: 500px;
  height: 300px;
  border: 1px solid;
  margin: 50px auto;
  padding: 50px;
  display: flex;
  align-items: center;
  justify-content: space-around;
  flex-direction: column;
}

.card-city__name{

}

.card-city__temperature {
  font-size: 25px;
}
</style>