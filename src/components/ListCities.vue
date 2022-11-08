<template>
  <div>
    <ul class="cities-list">
      <li
        v-for="city in listCitiesRu" 
        :key="city"
        class="cities-list-item"
        @click="$emit('clickCity', city)"
      >
        {{ city }}
      </li>
    </ul>
  </div>  
</template>

<script>
export default {
  props: {
    listCitiesRu: {
      type: Array,
      required: true
    }
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
  display: block;
  border: 1px solid;
  padding: 10px 20px;
  width: 200px;
  text-align: center;
  cursor: pointer;
}

.cities-list-item:hover {
  background-color: bisque;
}
</style>