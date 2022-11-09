<template>
  <div>
    <div class="card-city">
      <h2 class="card-city__name">{{ dataSelectedCity.name }}</h2>
      <p class="card-city__temperature">Темпартура: {{ dataSelectedCity.temperature }} 	&#176;С</p>
    </div>
  </div>  
</template>

<script>
export default {
  props: {
    dataSelectedCity: {
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
  border-radius: 5px;
  margin: 50px auto;
  padding: 50px;
  display: flex;
  align-items: center;
  justify-content: space-around;
  flex-direction: column;

  /* -webkit-box-shadow: 0px 0px 10px 11px rgba(214,214,214,1);
  -moz-box-shadow: 0px 0px 10px 11px rgba(214,214,214,1);
  box-shadow: 0px 0px 10px 11px rgba(214 214 214,1);

  -webkit-box-shadow: 0px 0px 10px 8px rgba(255,0,255,0,37);
-moz-box-shadow: 0px 0px 10px 8px rgba(255,0,255,0,37);
box-shadow: 0px 0px 10px 8px rgba(255,0,255,0,37); */

-webkit-box-shadow: 0px 0px 12px 8px rgba(255,  255,  255, 0.26);
-moz-box-shadow: 0px 0px 12px 8px rgba(255,  255,  255, 0.26);
box-shadow: 0px 0px 12px 8px rgba(255,  255,  255, 0.26);
}

.card-city__name{
  text-align: center;
}

.card-city__temperature {
  font-size: 25px;
  text-align: center;
}

@media(max-width: 800px) {
  .card-city {
    width: 100%;
    height: 200px;
    padding: 20px;
    margin-top: 20px;
  }

  .card-city__temperature {
    font-size: 20px;
  }

  .card-city {
    -webkit-box-shadow: 0px 0px 12px 4px rgba(255,  255,  255, 0.15);
    -moz-box-shadow: 0px 0px 12px 4px rgba(255,  255,  255, 0.15);
    box-shadow: 0px 0px 12px 4px rgba(255,  255,  255, 0.15);
  }
}
</style>