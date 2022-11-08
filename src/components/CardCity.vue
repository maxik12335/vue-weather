<template>
  <div>
    <div class="card-city">
      <h2 class="card-city__title">{{ title }}</h2>
      <p class="card-city__temperature">{{ temperature }}</p>
    </div>
  </div>  
</template>

<script>
export default {
  props: {
    title: "",
    temperature: "",
  }
}
</script>

<style>
.card-city {

}

.card-city__title {

}

.card-city__temperature {

}
</style>