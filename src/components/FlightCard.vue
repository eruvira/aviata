<script setup lang="ts"></script>

<template>
  <div class="flex flight-card rounded">
    <div class="bg-white pt-10 pb-5 px-11 w-9/12">
      <div class="flex items-center justify-between mb-[16px] mb-[50px] gap-5">
        <div class="flex items-center gap-3">
          <img
            src="https://aviata.kz/static/airline-logos/80x80/KC.png"
            class="h-5"
          />
          <p class="font-semibold text-base leading-[19px]">Air Astana</p>
        </div>
        <div>
          <p class="text-xs">25 ноя, вс</p>
          <p class="font-semibold text-2xl leading-[33px]">23:50</p>
        </div>
        <div class="w-[37%] flex flex-col items-center">
          <div class="flex justify-between w-full mb-0.5">
            <p class="text-[10px] leading-[12px] uppercase text-[#B9B9B9]">
              ALA
            </p>
            <p class="text-[10px] leading-[12px] uppercase text-[#B9B9B9]">
              ALA
            </p>
          </div>
          <div class="w-full flex justify-between items-center relative">
            <div>
              <div
                class="bg-white h-[5px] w-[5px] rounded-full border border-[#B9B9B9] relative"
              ></div>
            </div>
            <hr class="w-full border-t border-[#B9B9B9]" />
            <div
              class="bg-white h-[5px] w-[5px] rounded-full border border-[#B9B9B9]"
            ></div>
          </div>

          <p class="text-sm text-[#FF9900] mt-0.5 break-words">через Шымкент, 1 ч 60 м</p>
        </div>
        <div>
          <p class="text-xs flex">
            26 ноя, сб
            <span
              class="text-[10px] leading-[14px] text-[#FF3724] font-semibold pl-0.5"
              >+1</span
            >
          </p>
          <p class="font-semibold text-2xl leading-[33px]">03:45</p>
        </div>
      </div>
      <div class="flex">
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
        <div class="flex gap-1.5 items-center">
          <img src="../assets/irrevocable.svg" />
          <p class="text-xs text-[#707276]">невозвратный</p>
        </div>
      </div>
    </div>
    <div
      class="bg-[#F5F5F5] flex flex-col items-center px-5 pt-3 pb-[15px] w-4/12"
    >
      <p class="text-2xl leading-7 mb-[13px]">590 240 ₸</p>
      <button
        class="text-white font-bold text-lg leading-[25px] py-2 bg-[#55BB06] w-full rounded mb-2"
      >
        Выбрать
      </button>
      <p class="text-xs text-[#707276] mb-3">Цена за всех пассажиров</p>
      <div class="flex gap-x-1.5 justify-end w-full">
        <p class="text-xs m-auto">Нет багажа</p>
        <button
          class="bg-[#EAF0FA] text-[#5763B3] font-semibold text-xs py-[3px] px-2 rounded-sm"
        >
          + Добавить багаж
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped></style>