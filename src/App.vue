<script setup lang="ts">
import FilterOptions from "./components/FilterOptions.vue";
import FilterCompanies from "./components/FilterCompanies.vue";
import FlightCard from "./components/FlightCard.vue";
</script>

<template>
  <div class="grid pt-[50px] m-auto gap-5 main-page lg:max-w-[1140px] lg:px-0 pb-6">
    <div class="flex flex-col gap-3">
      <FilterOptions />
      <FilterCompanies />
      <button class="text-xs text-[#7284E4] border-b-[1px] border-dashed border-[#7284E4] pb-0.5 leading-3 h-fit w-fit">Сбросить все фильтры</button>
    </div>
    <div class="flex flex-col gap-3">
      <FlightCard />
      <FlightCard />
      <FlightCard /> <FlightCard /> <FlightCard /> <FlightCard /> <FlightCard /> <FlightCard /> <FlightCard />
      <FlightCard />
    </div>
  </div>
</template>

<style scoped>
.main-page{
  grid-template-columns: 0.8fr 3fr;
}
</style>
