<script>
  import axios from 'axios'

  export default {
    data() {
      return {
        city: "",
        error: "",
        info: null
      }
    },
    computed: {
      cityName() {
        return this.city
      },
      showTemp() {
        return "Temperature: " + this.info.main.temp
      },
      showFeelsLike() {
        return "Feels like: " + this.info.main.feels_like
      },
      showMinTemp() {
        return "Minimal temperature: " + this.info.main.temp_min
      },
      showMaxTemp() {
        return "Maximum temprature: " + this.info.main.temp_max
      }
    },
    methods: {
      getWeather() {
        if(this.city.trim().length < 2) {
          this.error = "Enter more then 2 symbols"
          return false
        }

        this.error = ""

        axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=d20c5a0d85b37f8dc8bbf72e66221a41`)
          .then(res => (this.info = res.data))
      }
    }
  }
</script>

<template>
  <div class="container">
    <h1>Weather App</h1>
    <p>Check the weather in {{ city == "" ? "your city" : cityName }}</p>
    <input type="text" v-model="city" placeholder="Enter the name of city">
    <p className = "error-message">{{ error }}</p>
    <button v-if="city != ''" @click="getWeather()">Check the weather</button>
    <button disabled v-else>No Way</button>

    <div v-if="info != null" className="extension-info">
      <p className="show-temp">{{ showTemp }}</p>
      <p className="show-feels-like">{{ showFeelsLike }}</p>
      <p className="show-min-temp">{{ showMinTemp }}</p>
      <p className="show-max-temp">{{ showMaxTemp }}</p>
    </div>
    
  </div>
</template>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&family=Oswald:wght@200..700&display=swap'); /* Montserrat and Oswald */

 .container {
  width: 900px;
  height: 500px;
  padding: 40px 20px;
  border-radius: 30px;
  background: #3a1e88;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: Montserrat;
  color: rgb(255, 247, 254);
 }

 .container h1:first-of-type {
  font-weight: 700;
  font-size: 60px;
 }

 .container p:first-of-type {
  font-weight: 500;
  font-size: 24px;
  margin-top: 20px;
  margin-bottom: 30px;
 }

 .error-message {
  font-weight: 400;
  font-size: 18px;
  color: #e91b1b;
  margin-top: 10px;
 }

 .container input {
  margin-top: 30px;
  width: 200px;
  height: 40px;
  background: transparent;
  border: 0;
  text-align: center;
  font-size: 18px;
  color: aliceblue;
  border-bottom: 1px solid #050308;
 }

 .container input:hover {
  border-bottom: 3px solid #050308;
 }

 .container button {
  margin-top: 20px;
  width: 150px;
  height: 50px;
  text-align: center;
  background: rgb(208, 255, 0);
  border-radius: 30px;
  border: 0;
  cursor: pointer;
 }
 
 .container button:hover {
  opacity: 0.5;
 }

 .container button:disabled {
  opacity: 1;
  background: #7a7a7a;
}


</style>