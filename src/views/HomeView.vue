<template>
  <main class="container text-white">
    <div class="pt-4 mb-8 relative">
      <input type="text"
             v-model="searchQuery"
             @input="getSearchResults"

             placeholder="Search for a city"
             class="py-2 px-1 w-full bg-transparent
border-b focus:border-weather-secondary focus:outline-none"/>
      <ul
          v-if="searchResults"
          class="absolute bg-weather-secondary text-white w-full shadow-md py-2 px-1
top-[66px] ">
        <p v-if="searchError">Error</p>
        <p v-if="searchResults.length === 0">Nothing to find...</p>
        <template v-else>
          <li v-for="searchResult in searchResults" :key="searchResult"
              class="py-2 cursor-pointer">
            {{ searchResult.place_name }}
          </li>
        </template>

      </ul>

    </div>
  </main>
</template>

<script setup>
import {ref} from "vue";
import axios from "axios";


const apiKey = "pk.eyJ1Ijoid2luc3RvbnNtaXRoMTMiLCJhIjoiY2w5eWc3aWp5MDR0YzNybHR0aHpwZXA0MSJ9.X7ftxw-Fo-r7l7MPDgSaww";
const searchQuery = ref("");
const queryTimeout = ref(null);
let searchResults = ref(null);
const searchError = ref(null);

const getSearchResults = () => {
  clearTimeout(queryTimeout.value);
  queryTimeout.value = setTimeout(async () => {
    if (searchQuery.value !== "") {
      try {
        const result = await axios.get(`https://api.mapbox.com/geocoding/v5/mapbox.places/${searchQuery.value}.json?access_token=${apiKey}&types=place`
        );
        searchResults.value = result.data.features;
      } catch {
        searchError.value = true;
      }

      return;
    }
    searchResults.value = null;
  }, 300)
}
</script>
