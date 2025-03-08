<template>
    <div class="container">
        <main>
        <h1>Weather App</h1> <br>
        <input type="text" v-model="city" placeholder="Enter a City..."> <br>
        <button @click="fetchData()">Enter</button>
        <br><br>
        <h3 v-if="temperature !== null">Temperature : {{ temperature }} &deg;C</h3>
        <h3 v-if="condition">Condition : {{ condition }}</h3>
        <img v-if="condition" :src="weatherPic" alt="Images">
        </main>
    </div>
</template>

<script>
import axios from "axios";
export default {
  data(){
    return{
        api_key : "76d8835c3f9a5fa68446874eb0c12490",
        city : "",
        temperature : null,
        condition : "",
        weatherPic: ""
    }
  },
  methods:{
    async fetchData(){
          const url = `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=${this.api_key}`;
          const response = await axios.get(url);
          try {
             this.temperature = response.data.main.temp;
             this.setWeather(response.data.weather[0].main,this.temperature);
            } catch (error){
               alert("City not Found");
            }
    },
    setWeather(Wcondition,temp){
        if(Wcondition.includes("Rain")){
              this.condition = "Rain";
              this.weatherPic = "../src/assets/rain.png"
        } else if (Wcondition.includes("Clouds")){
            this.condition= "Cloudy";
            this.weatherPic = "../src/assets/cloud.png"
        } else if (Wcondition.includes("Mist")){
            this.codition = "Misty";
            this.weatherPic = "../src/assets/mist.png";
        } else if (temp > 23){
            this.condition = "Hot";
            this.weatherPic = "../src/assets/clear.png"
        } else {
            this.condition = "Cold";
            this.weatherPic = "../src/assets/snow.png";
        }

    }
  }
}
</script>

<style scoped>
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.container{
    text-align: center;
    height: 70vh;
    width: 450px;
    margin: 0 auto;
    background: url("../src/assets/back.png");
    background-size: 100% 100%;
    border-radius: 13px;
    box-shadow: 0px 0px 15px rgba(0,0,0,0.26);
}
.container:hover{
    box-shadow: 0px 0px 30px rgba(0,0,0,0.53);
}
img{
    height: 200px;
    width: 200px;
}
h1{
    font-family: monospace;
    font-size: 47px;
    color: rgb(15, 236, 33);
}    
input {
    border-radius: 0px 8px 0px 8px;
    color:rgba(0,0,0,0.9);
    background-color: rgba(255,255,255,0.2);
    height: 4%;
    width: 60%;
    border: none;
    padding: 20px;
    font-size: 25px;
    font-family:   Geneva, Verdana, sans-serif;
}
input:focus{
    border: 3px solid black;
    border-radius: 8px 0px 8px 0px;
    transition: ease-in;
    height: 5%;
    background-color: rgba(240,248,250,0.6);
}
button{
    margin-top: 17px;
    width: 22%;
    height: 6%;
    background-color: rgba(229, 40, 40, 0.4);
    border: 2px solid pink;
    color: bisque;
    font-size: 18px;
    font-weight: bolder;
    border-radius: 5px;
}
button:hover{
    background: blue;
    cursor: pointer;
}
h3{
    font-family:   Verdana, Geneva, Tahoma, sans-serif;
    color: rgba(255,223,114,0.9);
    font-size: 22px;
    padding: 12px;
    margin-top: 12px;
}
main{
    background: linear-gradient(to bottom,rgba(0,0,0,0.5),rgba(0,0,0,0.75));
    height: 100%;
    border-radius: 13px;
}
@media screen and (max-width:1024px){
    .container{
    text-align: center;
    height: 70vh;
    width: 60%;
    margin: 0 auto;
    background: url("../src/assets/back.png");
    background-size: 100% 100%;
    border-radius: 13px;
    box-shadow: 0px 0px 15px rgba(0,0,0,0.26);
}
}
</style>