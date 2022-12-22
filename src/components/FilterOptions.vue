<template>
  <div class="bg-[#F5F5F5] rounded w-full">
    <div class="flex mb-3 justify-between items-center pt-3 px-3">
      <h2 class="font-bold text-sm">Опции тарифа</h2>
      <div class="custom-tooltip relative inline-block cursor-pointer">
        <svg
          width="20"
          height="20"
          viewBox="0 0 20 20"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M10.6464 8.64648L13.2929 6.00004L10.6464 3.35359L11.3535 2.64648L14 5.29293L16.6464 2.64648L17.3535 3.35359L14.7071 6.00004L17.3535 8.64648L16.6464 9.35359L14 6.70714L11.3535 9.35359L10.6464 8.64648ZM2.91465 6.00003H8C8 6.34074 8.0284 6.67482 8.08296 7.00003H2.91465C2.70873 7.58263 2.15311 8.00003 1.5 8.00003C0.671573 8.00003 0 7.32846 0 6.50003C0 5.6716 0.671573 5.00003 1.5 5.00003C2.15311 5.00003 2.70873 5.41743 2.91465 6.00003ZM7.91465 10H9.52779C9.86799 10.3801 10.2559 10.7166 10.6822 11H7.91465C7.70873 11.5826 7.15311 12 6.5 12C5.84689 12 5.29127 11.5826 5.08535 11H0.5C0.223858 11 0 10.7762 0 10.5C0 10.2239 0.223858 10 0.5 10H5.08535C5.29127 9.41743 5.84689 9.00003 6.5 9.00003C7.15311 9.00003 7.70873 9.41743 7.91465 10ZM2.91465 14C2.70873 13.4174 2.15311 13 1.5 13C0.671573 13 0 13.6716 0 14.5C0 15.3285 0.671573 16 1.5 16C2.15311 16 2.70873 15.5826 2.91465 15H14.5C14.7761 15 15 14.7762 15 14.5C15 14.2239 14.7761 14 14.5 14H2.91465Z"
            fill="#B9B9B9"
          />
        </svg>
        <span class="tooltip-text bg-white text-xs border-[#E1E1E1] absolute p-3 w-max rounded-md border left-2/4 bottom-[175%] ml-[-60px]">Сбросить выбор</span>
      </div>
    </div>
    <div class="pb-3">
      <label class="custom-checkbox text-xs flex items-center px-3 hover:bg-[#EBEBEB]">
        Только прямые
        <input type="checkbox" />
        <span class="custom-box"> </span>
      </label>
      <label class="custom-checkbox text-xs flex items-center px-3 hover:bg-[#EBEBEB]">
        Только с багажом
        <input type="checkbox" />
        <span class="custom-box"> </span>
      </label>
      <label class="custom-checkbox text-xs flex items-center px-3 hover:bg-[#EBEBEB]">
        Только возвратные
        <input type="checkbox" />
        <span class="custom-box"> </span>
      </label>
    </div>
  </div>
</template>

<style scoped>
.custom-checkbox {
  position: relative;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  padding-left: 36px;
  height: 32px;
}

.custom-checkbox input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.custom-box {
  position: absolute;
  top: 32%;
  left: 12px;
  width: 12px;
  height: 12px;
  background: white;
  border: 1px solid #b9b9b9;
  border-radius: 2px;
}

.custom-box:after {
  content: "";
  position: absolute;
  display: none;
}

.custom-checkbox:hover input ~ .custom-box:after {
  left: 2px;
  top: -0.5px;
  width: 5px;
  height: 7px;
  border: solid #b9b9b9;
  border-width: 0 2.5px 2.5px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
  display: block;
}

.custom-checkbox input:checked ~ .custom-box:after {
  display: block;
  left: 2px;
  top: -0.5px;
  width: 5px;
  height: 7px;
  border: solid white;
  border-width: 0 2.5px 2.5px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}

.custom-checkbox input:checked ~ .custom-box {
  background: #55bb06;
  border: 1px solid #55bb06;
}

.custom-tooltip:hover path {
  fill: #7284e4;
}


.tooltip-text {
  visibility: hidden;
  text-align: center;
  opacity: 0;
  transition: opacity 0.3s;
}

.custom-tooltip .tooltip-text::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: white transparent transparent transparent;
}

.custom-tooltip .tooltip-text::before {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: -6px;
  border-width: 6px;
  border-style: solid;
  border-color: #e5e5e5 transparent transparent transparent;
}

.custom-tooltip:hover .tooltip-text {
  visibility: visible;
  opacity: 1;
}
</style>
