<script setup lang="ts">
import { computed, isReadonly } from "vue";
const props = defineProps<{
  hop: any;
}>();

const options = { day: "numeric", month: "short" };
const weekday = { weekday: "short" };

const imgPath = computed(() => {
  return `https://aviata.kz/static/airline-logos/80x80/${props.hop.validating_carrier}.png`;
});

const depDate = computed(() => {
  return new Date(props.hop.itineraries[0][0].segments[0].dep_time_iso)
    .toLocaleString("ru-RU", options)
    .slice(0, -1);
});

const depDateWeekday = computed(() => {
  return new Date(
    props.hop.itineraries[0][0].segments[0].dep_time_iso
  ).toLocaleString("ru-RU", weekday);
});

const arrDate = computed(() => {
  return new Date(
    props.hop.itineraries[0][0].segments[
      props.hop.itineraries[0][0].segments.length - 1
    ].arr_time_iso
  )
    .toLocaleString("ru-RU", options)
    .slice(0, -1);
});

const arrDateWeekday = computed(() => {
  return new Date(
    props.hop.itineraries[0][0].segments[0].arr_time_iso
  ).toLocaleString("ru-RU", weekday);
});

const depTime = computed(() => {
  let date = props.hop.itineraries[0][0].dep_date.split(" ")[1];
  if (date.length < 5) return "0" + date;
  return date;
});

const arrTime = computed(() => {
  let date = props.hop.itineraries[0][0].arr_date.split(" ")[1];
  if (date.length < 5) return "0" + date;
  return date;
});

const getIsDay = computed(() => {
  let depDate = new Date(props.hop.itineraries[0][0].dep_date.split(" ")[0]);
  let arrDate = new Date(props.hop.itineraries[0][0].arr_date.split(" ")[0]);
  const diff = (arrDate.valueOf() - depDate.valueOf()) / (1000 * 60 * 60 * 24);
  if (diff > 0) return "+" + diff;
});

const secsToTime = function(secs: number){
  let minutesAll = Math.floor(secs / 60);
  let hours = Math.floor(minutesAll / 60);
  let minutes = minutesAll % 60;
  return hours + " " + "ч" + " " + minutes + " " + "м";
}
</script>

<template>
  <div class="flex flight-card rounded flex-col lg:flex-row">
    <div
      class="bg-white w-full rounded-t pt-[18px] px-5 lg:pt-10 lg:pb-5 lg:pl-11 lg:w-9/12 lg:rounded-tl lg:rounded-bl lg:rounded-tr-none"
    >
      <div
        class="flex flex-col lg:flex-row lg:items-center lg:justify-start lg:mb-[50px]"
      >
        <div class="mr-auto flex justify-between w-full lg:w-[23%]">
          <div class="flex items-center gap-3">
            <img :src="imgPath" class="h-5" />
            <p class="font-semibold text-base leading-[19px]">
              {{ hop.itineraries[0][0].carrier_name }}
            </p>
          </div>
          <p
            v-if="
              hop.itineraries[0][0].segments[0].baggage_options[0].value > 0
            "
            class="text-xs lg:hidden"
          >
            {{ hop.itineraries[0][0].segments[0].baggage_options[0].value }} {{ hop.itineraries[0][0].segments[0].baggage_options[0].unit === 'KG' ? 'кг' : 'штука' }}
          </p>
          <p v-else class="text-xs lg:hidden">Нет багажа</p>
        </div>
        <div class="hidden mr-auto lg:block">
          <p class="text-xs">{{ depDate }}, {{ depDateWeekday }}</p>
          <p class="font-semibold text-2xl leading-[33px]">{{ depTime }}</p>
        </div>
        <div class="flex justify-between mt-6 mb-[32px] lg:hidden">
          <div>
            <p class="text-xs">{{ depDate }}, {{ depDateWeekday }}</p>
            <p class="font-semibold text-2xl leading-[33px]">{{ depTime }}</p>
          </div>
          <div>
            <p class="text-xs flex">
              {{ arrDate }}, {{ arrDateWeekday }}
              <span
                class="text-[10px] leading-[14px] text-[#FF3724] font-semibold pl-[5px]"
                >{{ getIsDay }}</span
              >
            </p>
            <p class="font-semibold text-2xl leading-[33px]">{{ arrTime }}</p>
          </div>
        </div>
        <div class="w-full lg:w-[37%] flex flex-col items-center mr-auto">
          <div class="flex justify-between w-full mb-0.5">
            <p class="text-[10px] leading-[12px] uppercase text-[#B9B9B9]">
              {{ hop.itineraries[0][0].segments[0].origin_code }}
            </p>
            <p class="text-xs leading-[18px]">{{ secsToTime(props.hop.itineraries[0][0].traveltime) }}</p>
            <p class="text-[10px] leading-[12px] uppercase text-[#B9B9B9]">
              {{
                hop.itineraries[0][0].segments[
                  hop.itineraries[0][0].segments.length - 1
                ].dest_code
              }}
            </p>
          </div>
          <div class="w-full flex justify-between items-center relative">
            <div class="flex justify-between w-full absolute">
              <div
                class="bg-white h-[5px] w-[5px] rounded-full border border-[#B9B9B9]"
              ></div>

              <div
                v-for="index in hop.itineraries[0][0].stops"
                :key="index"
                class="bg-white h-[5px] w-[5px] rounded-full border border-[#B9B9B9]"
              ></div>
              <div
                class="bg-white h-[5px] w-[5px] rounded-full border border-[#B9B9B9]"
              ></div>
            </div>
            <hr class="w-full border-t border-[#B9B9B9]" />
          </div>

          <p
            v-for="index in hop.itineraries[0][0].stops" :key="index"
            class="text-[12px] text-[#FF9900] mt-4 mb-[30px] lg:mt-0.5 lg:mb-0"
          >
            через {{  hop.itineraries[0][0].segments[index-1].dest }}, {{ secsToTime(hop.itineraries[0][0].layovers[index-1]) }}
          </p>
        </div>

        <div class="hidden mr-auto lg:block">
          <p class="text-xs flex">
            {{ arrDate }}, {{ arrDateWeekday }}
            <span
              class="text-[10px] leading-[14px] text-[#FF3724] font-semibold pl-0.5"
              >{{ getIsDay }}</span
            >
          </p>
          <p class="font-semibold text-2xl leading-[33px]">{{ arrTime }}</p>
        </div>
      </div>
      <div class="hidden lg:flex">
        <button
          class="text-xs text-[#7284E4] border-b-[1px] border-dashed border-[#7284E4] pb-0.5 leading-3 h-fit mr-[23px]"
        >
          Детали перелета
        </button>
        <button
          class="text-xs text-[#7284E4] border-b-[1px] border-dashed border-[#7284E4] pb-0.5 leading-3 h-fit mr-[46px]"
        >
          Условия тарифа
        </button>
        <div
          v-if="!hop.itineraries[0][0].refundable"
          class="flex gap-1.5 items-center"
        >
          <img src="../assets/irrevocable.svg" />
          <p class="text-xs text-[#707276]">невозвратный</p>
        </div>
      </div>
    </div>
    <div
      class="bg-[#F5F5F5] rounded-b w-fill flex flex-col items-center px-5 pt-3 pb-[15px] lg:w-4/12 lg:rounded-tr lg:rounded-br lg:rounded-bl-none"
    >
      <p class="text-2xl leading-7 mb-[13px]">{{ hop.price }} ₸</p>
      <button
        class="text-white font-bold text-lg leading-[25px] py-2 bg-[#55BB06] w-full rounded mb-[14px] lg:mb-2"
      >
        Выбрать
      </button>
      <p class="text-xs text-[#707276] lg:mb-3">Цена за всех пассажиров</p>
      <div class="hidden lg:justify-end lg:w-full lg:flex">
        <p
          v-if="hop.itineraries[0][0].segments[0].baggage_options[0].value > 0"
          class="text-xs m-auto"
        >
          {{ hop.itineraries[0][0].segments[0].baggage_options[0].value }} {{ hop.itineraries[0][0].segments[0].baggage_options[0].unit === 'KG' ? 'кг' : 'штука' }}
        </p>
        <p v-else class="text-xs m-auto">Нет багажа</p>
        <button
          class="bg-[#EAF0FA] text-[#5763B3] font-semibold text-xs py-[3px] px-2 rounded-sm"
        >
          + Добавить багаж
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.flight-card {
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.15);
}
</style>
