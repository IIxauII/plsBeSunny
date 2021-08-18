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
            this.temperature = Math.round(data.main.temp) + ' °C';
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
            // This key should be exported into a config file
            const key = 'enterYourPersonalApiKeyHere';
            const apiString = 'https://api.openweathermap.org/data/2.5/weather?lat=' + lat + '&lon=' + lon + '&appid=' + key + '&units=metric';
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
/* gujarati */
@font-face {
    font-family: 'Farsan';
    font-style: normal;
    font-weight: 400;
    src: local('Farsan Regular'), local('Farsan-Regular'), url('../assets/css/fonts/VEMwRoJ0vY_zsyzKxqWo5jbtrMOL.woff2') format('woff2');
    unicode-range: U+0964-0965, U+0A80-0AFF, U+200C-200D, U+20B9, U+25CC, U+A830-A839;
}
/* vietnamese */
@font-face {
    font-family: 'Farsan';
    font-style: normal;
    font-weight: 400;
    src: local('Farsan Regular'), local('Farsan-Regular'), url('../assets/css/fonts/VEMwRoJ0vY_zsyzK0qWo5jbtrMOL.woff2') format('woff2');
    unicode-range: U+0102-0103, U+0110-0111, U+1EA0-1EF9, U+20AB;
}
/* latin-ext */
@font-face {
    font-family: 'Farsan';
    font-style: normal;
    font-weight: 400;
    src: local('Farsan Regular'), local('Farsan-Regular'), url('../assets/css/fonts/VEMwRoJ0vY_zsyzK06Wo5jbtrMOL.woff2') format('woff2');
    unicode-range: U+0100-024F, U+0259, U+1E00-1EFF, U+2020, U+20A0-20AB, U+20AD-20CF, U+2113, U+2C60-2C7F, U+A720-A7FF;
}
/* latin */
@font-face {
    font-family: 'Farsan';
    font-style: normal;
    font-weight: 400;
    src: local('Farsan Regular'), local('Farsan-Regular'), url('../assets/css/fonts/VEMwRoJ0vY_zsyzK3aWo5jbtrA.woff2') format('woff2');
    unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212,
        U+2215, U+FEFF, U+FFFD;
}
/* gujarati */
@font-face {
    font-family: 'Shrikhand';
    font-style: normal;
    font-weight: 400;
    src: local('Shrikhand Regular'), local('Shrikhand-Regular'), url('../assets/css/fonts/a8IbNovtLWfR7T7bMJwrGIKR8Ttcte1q.woff2') format('woff2');
    unicode-range: U+0964-0965, U+0A80-0AFF, U+200C-200D, U+20B9, U+25CC, U+A830-A839;
}
/* latin-ext */
@font-face {
    font-family: 'Shrikhand';
    font-style: normal;
    font-weight: 400;
    src: local('Shrikhand Regular'), local('Shrikhand-Regular'), url('../assets/css/fonts/a8IbNovtLWfR7T7bMJwrDYKR8Ttcte1q.woff2') format('woff2');
    unicode-range: U+0100-024F, U+0259, U+1E00-1EFF, U+2020, U+20A0-20AB, U+20AD-20CF, U+2113, U+2C60-2C7F, U+A720-A7FF;
}
/* latin */
@font-face {
    font-family: 'Shrikhand';
    font-style: normal;
    font-weight: 400;
    src: local('Shrikhand Regular'), local('Shrikhand-Regular'), url('../assets/css/fonts/a8IbNovtLWfR7T7bMJwrA4KR8TtctQ.woff2') format('woff2');
    unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212,
        U+2215, U+FEFF, U+FFFD;
}
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
