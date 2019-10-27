<template>
    <div class="container mt-5 text-center">
        <h1 class="text-center">Weather Portal</h1>
        <div class="input-group mt-5">
            <input id="regionQuerySearch" v-model="regionQuerySearch" class="form-control" type="text" placeholder="Type your region">
            <div class="input-group-append"><button class="btn btn-primary" v-on:click="getWeatherData">View Weather</button></div>
        </div>
        <div v-if="weatherList.length == 0">
            
        </div>
        <div v-else>
            <div class="jumbotron mt-5">
                <h2>{{weatherList.name}}, {{weatherList.sys.country}}</h2>
                <h3>{{weatherList.weather[2]}}</h3>
                <div class="row mt-5">
                    <div class="col-4">
                        <h3>Temperature</h3>
                        <h4>{{getCelcius()}} C</h4>
                    </div>
                    <div class="col-4">
                        <h3>Wind Speed</h3>
                        <h4>{{weatherList.wind.speed}}</h4>
                    </div>
                    <div class="col-4">
                        <h3>Humidity</h3>
                        <h4>{{weatherList.main.humidity}}</h4>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'WeatherApp',
    regionQuerySearch: String,
    data() {
        return{
            weatherList: [],
        };
    },
    methods: {
        getWeatherData(){
            axios.get("https://api.openweathermap.org/data/2.5/weather?q="+ this.regionQuerySearch + "&appid=2c7b5435fb3752e727ae7f4e085ee776").then(res => (this.weatherList = res.data));
        },
        getCelcius(){
            return (this.weatherList.main.temp - 273.15).toFixed(2);
        }
    }
}
</script>