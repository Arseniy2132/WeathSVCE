<script>
import axios from 'axios'
export default {
    data(){
      return {
        city: "",
        error: "",
        info: null,
        dele: ""
      }
    },
    
    methods:{
 getWeather(){
        if(this.city.trim().length < 2){
          this.error = "Введите корректное название города"
          return false
        }
        this.error = ""

        axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=17ff3901709ef46816d36036b474961d`)
          .then(res => (this.info = res.data))
          this.dele = (`Температура:   ${this.info.main.temp},
          Ощущается как:   ${this.info.main.feels_like},
          Минмальная температура:   ${this.info.main.temp_min},
          Максимальная температура:   ${this.info.main.temp_max}`)
          

        

      },
      deleteUser(){
        this.dele = ""
      },

    }

}
</script>

<template>
  <div class="wrapper">
    <h1>Погодное приложение </h1>
    <p>Узнать погоду в {{ city == ""? "вашем городе" : cityName }}</p>
    <input type="text" v-model="city" placeholder="Введите город">
    <button v-if="city !=''" @click="getWeather">Получить погоду</button>
    <button  disabled v-else>Введите название города</button> <br>
     <p v-if="info !=null">

 {{ dele }}
     </p>
    <p class="error">{{ error }}</p>
    <button @click="deleteUser">Очистить данные</button></div>

    <!--<div v-if="info !=null">
      <p v-show="info !=null">{{ showTemp }}</p>
      <p v-show="info !=null">{{ showFeelsLike }}</p>
      <p v-show="info !=null">{{ showMinTemp }}</p>
      <p v-show="info !=null">{{ showMaxTemp }}</p>
      

  </div>-->

</template>

<style scoped>

.error{
  color: red;
}
.wrapper{
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background: #1f0f24;
  text-align: center;
  color: #fff;
}

.wrapper h1{
  margin-top: 50px;
}
.wrapper p{
  margin-top: 20px;
}
.wrapper input{
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;

}
.wrapper input:focus{
  border-bottom-color: #6e2d7d;
}
.wrapper button:disabled{
  background: #635325;
  cursor: not-allowed;
}
.wrapper button{
  background: #e3bc4b;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;

  transition: transform 500ms ease;
}
.wrapper button:hover{
  transform: scale(1.1) translateY(-5px);
}
</style>
