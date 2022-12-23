<script setup lang="ts">
import FilterOptions from "./components/FilterOptions.vue";
import FilterCompanies from "./components/FilterCompanies.vue";
import FlightCard from "./components/FlightCard.vue";
import data from './assets/results.json' 

const airlines = data.airlines
const flights = data.flights
</script>

<template>
  <div class="lg:grid pt-4 px-4 pb-5 m-auto gap-5 main-page xl:max-w-[1140px] xl:px-0 xl:lg:pt-[50px]">
    <div class="flex flex-col gap-3 mb-[23px]">
      <FilterOptions />
      <FilterCompanies :companies="airlines"/>
      <button class="text-xs text-[#7284E4] border-b-[1px] border-dashed border-[#7284E4] pb-0.5 leading-3 h-fit w-fit">Сбросить все фильтры</button>
    </div>
    <div class="flex flex-col gap-3">
      <FlightCard v-for="(flight, index) in flights" :key="'flight'+index" :hop="flight"/>
    </div>
  </div>
</template>

<style scoped>
.main-page{
  grid-template-columns: 0.8fr 3fr;
}

</style>
