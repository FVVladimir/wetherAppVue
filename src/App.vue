<template>
  <div class="wrapper">
      <h1> Wether </h1>
      <p> wether in {{ city == "" ? "your city" : cityName}} </p>
      <input type="text" 
      v-model = "city" 
      placeholder="enter city name"/>
      <button v-show="city != ''" v-on:click="getWether()"> get wether </button>
      <p class="error">{{ error }}</p>
     <div  v-if = "info != null">
        <p>{{ showTemp }}</p>       
        <p>{{ showPressure }}</p>
        <p>{{ showHumidity }}</p>
     </div>
     
     
      
  </div>
</template>

<script>

  import axios from 'axios'
  export default {
    data(){
      return {
        city: "",
        error:"",
        info: null
      }
    },
    computed: {
      cityName(){
        return "< " + this.city + " >"
      },      
      showTemp() {
        return "температура повітря " + this.info.temp;
      },
      showPressure() {
        return "атмосферний тиск " + this.info.pressure;
      },
      showHumidity() {
        return "вологість " + this.info.humidity;
      }

    },
    methods:{
      getWether(){
         axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=fb365b8ac5490c379335ae772bf1f912`)
          .then(res => (this.info = res.data.main))
      }
    }
  }
</script>

<style scoped>
   h1 {
    color: red;
   }
</style>