<template>
    <div class="weather">
        <div class="container">
            <point-city @indicateCity="indicateCity"></point-city>
            <weather-block :weatherInfo="weatherInfo"></weather-block>
        </div>
    </div>
</template>

<script>
/* eslint-disable */
import '@/assets/styles/normalize.css'
import axios from 'axios';
import WeatherBlock from '@/components/WeatherBlock'
import PointCity from '@/components/PointCity'
export default {
    components: {
        WeatherBlock, PointCity
    },
    data(){
        return {
            weatherInfo: {
                city: '',
                temperature: '',
                wind: 0,
                weather: '',
                description: '',
                imgCode: '',
                error: false,
                show: false
            }
        }
    },
    methods: {
        async fetchWeather(city){
            try {
                const responseCoordinates = await axios.get(`http://api.openweathermap.org/geo/1.0/direct?q=${city}&limit=5&appid=b6a9838954657b16d85a7ac99625614c`);
                this.weatherInfo.city = city;
                if(responseCoordinates.data.length === 0){
                    this.weatherInfo.show = false;
                    this.weatherInfo.error = true;
                    return
                } else {
                    this.weatherInfo.error = false;
                    this.weatherInfo.show = true;
                    const responseWeather = await axios.get(`http://api.openweathermap.org/data/2.5/weather?lat=${Math.round(responseCoordinates.data[0].lat)}&lon=${Math.round(responseCoordinates.data[0].lon)}&appid=b6a9838954657b16d85a7ac99625614c&units=metric&lang=ru`);
                    const dataWeather = responseWeather.data;
                    this.weatherInfo.temperature = Math.round(dataWeather.main.temp) + '°C';
                    this.weatherInfo.weather = dataWeather.weather[0].description[0].toUpperCase() + dataWeather.weather[0].description.slice(1);
                    this.weatherInfo.wind = dataWeather.wind.speed;
                    this.weatherInfo.imgCode = dataWeather.weather[0].icon;
                }
            } catch (error) {
                console.log(error)
            }
        },
        indicateCity(city){
            this.fetchWeather(city)
        }
    }
}
</script>

<style lang="scss">
    .weather{
        font-family: 'Comfortaa', sans-serif;
        background-color: #eae4ca;
        min-height: 100vh;
    }
    .container{
        max-width: 768px;
        width: 100%;
        margin: 0 auto;
    }
</style>