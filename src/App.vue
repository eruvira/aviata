<script setup lang="ts">
import FilterOptions from "./components/FilterOptions.vue";
import FilterCompanies from "./components/FilterCompanies.vue";
import FlightCard from "./components/FlightCard.vue";
import data from "./assets/results.json";
import { ref } from "vue";

const airlines = data.airlines;
const flights = ref(data.flights);

const airlnesFilter = ref([])
const optionsFilter = ref([])

const getOptionsFilter = (filters: any) => {
  flights.value = data.flights
  optionsFilter.value = filters
  optionsSort(optionsFilter.value)
  airlinesSort(airlnesFilter.value)
}

const getAirlineFilters = (filters: any) => {
  flights.value = data.flights
  airlnesFilter.value = filters
  optionsSort(optionsFilter.value)
  airlinesSort(airlnesFilter.value)
}

const resetAll = () => {
  let airlinesBoxes = document.getElementsByClassName(
    "box"
  ) as HTMLCollectionOf<HTMLInputElement>;
  let optionsBoxes = document.getElementsByClassName(
    "opBox"
  ) as HTMLCollectionOf<HTMLInputElement>;
  for (let i = 0; i < airlinesBoxes.length; i++) {
    const checkbox = airlinesBoxes[i];
    checkbox.checked = false;
  }
  for (let i = 0; i < optionsBoxes.length; i++) {
    const checkbox = optionsBoxes[i];
    checkbox.checked = false;
  }
  flights.value = data.flights;
};

const optionsSort = (filter: any) => {
  if (filter.includes("direct")) {
    filterDirect();
  }
  if (filter.includes("baggage")) {
    filterBaggage();
  }
  if (filter.includes("returnable")) {
    filterReturnable();
  }
};

const filterDirect = () => {
  let sorted = []
  for(let i = 0; i < flights.value.length; i++){
    if(flights.value[i].itineraries[0][0].stops === 0){
      sorted.push(flights.value[i])
    }
  }
  flights.value = sorted
}

const filterBaggage = () => {
  let sorted = []
  for(let i = 0; i < flights.value.length; i++){
    if(flights.value[i].itineraries[0][0].segments[0].baggage_options[0].value > 0){
      sorted.push(flights.value[i])
    }
  }
  flights.value = sorted
}

const filterReturnable = () => {
  let sorted = []
  for(let i = 0; i < flights.value.length; i++){
    if(flights.value[i].itineraries[0][0].refundable === true){
      sorted.push(flights.value[i])
    }
  }
  flights.value = sorted
}

const airlinesSort = (filter: any) => {
  if (filter.length && !filter.includes("all")) {
    let filtred = [] as Array<any>;
    for (let i = 0; i < flights.value.length; i++) {
      for (let j = 0; j < filter.length; j++) {
        if (flights.value[i].validating_carrier === filter[j]) {
          filtred.push(flights.value[i]);
        }
      }
    }
    flights.value = filtred;
  }
};
</script>

<template>
  <div
    class="lg:grid pt-4 px-4 pb-5 m-auto gap-5 main-page xl:max-w-[1140px] xl:px-0 xl:lg:pt-[50px]"
  >
    <div class="flex flex-col gap-3 mb-[23px]">
      <FilterOptions @sortByOptions="getOptionsFilter" />
      <FilterCompanies :companies="airlines" @sortByAirlines="getAirlineFilters" />
      <button
        class="text-xs text-[#7284E4] border-b-[1px] border-dashed border-[#7284E4] pb-0.5 leading-3 h-fit w-fit"
        @click="resetAll"
      >
        Сбросить все фильтры
      </button>
    </div>
    <div class="flex flex-col gap-3">
      <FlightCard
        v-for="(flight, index) in flights"
        :key="'flight' + index"
        :hop="flight"
      />
      <div v-if="!flights.length" class="font-semibold bg-[#F5F5F5] rounded h-full flex justify-center items-center">
        По данному запросу результатов не найдено
      </div>
    </div>
  </div>
</template>

<style scoped>
.main-page {
  grid-template-columns: 0.8fr 3fr;
}
</style>
