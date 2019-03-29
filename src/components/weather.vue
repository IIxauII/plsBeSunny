<template lang="pug">
    div.weather
        div.weather__location
            | {{ location }}
        div.weather__icon
            i.weather__icon__img
        div.weather__temperature
            | {{ temperature }}
        div.weather__type
            | {{ type }}
</template>
<script>
const axios = require('axios');

export default {
    name: 'weather',
    data() {
        return {
            location: null,
            temperature: null,
            type: null,
        };
    },
    methods: {
        processWeatherData(data) {
            // eslint-disable-next-line
            console.log(data.name);
            // eslint-disable-next-line
            console.log(data.main.temp);
            // eslint-disable-next-line
            console.log(data.weather[0].description);
            // eslint-disable-next-line
            console.log(data.weather[0].icon);
            this.location = data.name;
            this.temperature = Math.round(data.main.temp) + ' C°';
            this.type = data.weather[0].description;
            const conditionCode = data.weather[0].id;
            const weatherImg = document.querySelector('.weather__icon__img');
            const weatherIcon = data.weather[0].icon;
            let weatherClassString = 'owf-' + conditionCode;
            if (weatherIcon.includes('n')) {
                weatherClassString += '-n';
            } else {
                weatherClassString += '-d';
            }
            weatherImg.classList.add('owf', weatherClassString);
            // eslint-disable-next-line
            console.log(this.location);
        },
        getWeather(apiString) {
            axios
                .get(apiString)
                .then((response) => {
                    this.processWeatherData(response.data);
                })
                .catch((error) => {
                    // eslint-disable-next-line
                    console.error(error);
                });
        },
        buildApiCall(lat, lon) {
            const key = '102313f616cf36cbc7fa381982977f2d';
            const apiString = 'http://api.openweathermap.org/data/2.5/weather?lat=' + lat + '&lon=' + lon + '&appid=' + key + '&units=metric';
            // eslint-disable-next-line
            console.log(apiString);
            this.getWeather(apiString);
        },
        getLocation() {
            navigator.geolocation.getCurrentPosition(async (position) => {
                const lat = position.coords.latitude;
                const lon = position.coords.longitude;
                this.buildApiCall(lat, lon);
            });
        },
    },
    mounted() {
        this.getLocation();
    },
};
</script>
<style lang="scss">
    @import url('https://fonts.googleapis.com/css?family=Farsan|Shrikhand');
    @import '../assets/css/owfont-master/css/owfont-regular.css';
    $colorRandom: rgb(random(255), random(255), random(255));
    .weather {
        display: flex;
        width: 100%;
        height: 100%;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
        font-family: 'Farsan', cursive;
        color: white;
        &__location,
        &__icon,
        &__temperature,
        &__type {
            flex-basis: 50%;
            align-self: center;
            text-align: center;
            font-size: 1.5rem;
        }
        &__location {
            order: 1;
            font-family: 'Shrikhand', cursive;
            font-size: 4rem;
            color: $colorRandom;
        }
        &__icon {
            order: 2;
            &__img {
                font-size: 4rem;
            }
        }
        &__temperature {
            order: 3;
        }
        &__type {
            order: 4;
        }
    }
</style>
