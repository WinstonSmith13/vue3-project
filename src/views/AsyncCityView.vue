<template>
  <div class="flex flex-col flex-1 items-center">
    <div
        v-if="route.query.preview"
        class="text-white p-4 bg-weather-secondary w-full text-center">
      You are currently previewing this city, click the "+"
      icon to start tracking this city.

    </div>
    <div class="text-4xl mb-2">
      <h1 class="text-4xl mb-2">{{ route.params.city }}</h1>
      <p class="text-8xl mb-8"> {{ Math.round(resultData.current.temp) }}</p>
    </div>

  </div>
</template>

<script setup>
import axios from "axios";
import {useRoute} from 'vue-router';

const apiOpenKey = '368b822416a6e5e5231d51ccde972e42';


const route = useRoute();
const getWeatherData = async () => {
  try {
    const resultData = await axios.get(`https://api.openweathermap.org/data/2.5/onecall?lat=${route.query.lat}&lon=${route.query.lng}&exclude={part}&units=metric&appid=${apiOpenKey}`);
    return resultData;
  } catch (err) {
    console.log(err);
  }
};
const weatherData = await getWeatherData();
console.log(weatherData);


</script>


