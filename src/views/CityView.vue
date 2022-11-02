<template>
  <div>
<suspense>
  <async-city-view/>
  <template #fallback>
    <p>Loading...</p>
  </template>
</suspense>


  </div>
</template>

<script setup>
import AsyncCityView from "./AsyncCityView.vue";

</script>

<style scoped>

</style>
