<script setup lang="ts">
import { ref } from "vue";
let showhistory = ref(true);
let number = ref("");
let showSideMune = ref(true);
let operator = ref();
let watch = ref();
let previos = ref();
let operatorclick = ref(false);

let history = ref([
  {
    number: "",
    result: "",
  },
]);
function delet(){
  history.value = []
}
function showMune() {
  showSideMune.value = !showSideMune.value;
}
function hideMuneHistoy() {
  showhistory.value = true;
  showSideMune.value = true;
}

function showHistory() {
  showhistory.value = false;
  console.log(showhistory.value);
}

function clear() {
  number.value = "";
  watch.value = "";
}

function action(n: string) {
  if (operatorclick.value === true) {
    number.value = "";
    operatorclick.value = false;
  }
  number.value += n;
}
function setprevios(o: string) {
  previos.value = number.value;
  operatorclick.value = true;
  watch.value = previos.value + o;
}

function percentage() {
  if (number.value === "") return;
  let result = parseFloat(number.value) / 100;
  number.value = result.toString();
}
function dot() {
  if (number.value.indexOf(".") === -1) {
    action(".");
  }
}
function remove() {
  number.value = number.value.slice(0, -1);
}

function equal() {
  watch.value += number.value;
  watch.value += " =";
  number.value = operator.value(
    parseFloat(previos.value),
    parseFloat(number.value)
  );
  history.value.push({
    number: watch.value,
    result: number.value.toString(),
  });
}
function plus() {
  operator.value = (a: number, b: number) => a + b;
  setprevios(" + ");
  console.log(operatorclick);
}
function divide() {
  operator.value = (a: number, b: number) => a / b;
  setprevios(" / ");
}
function multiply() {
  operator.value = (a: number, b: number) => a * b;
  setprevios(" * ");
}
function mines() {
  operator.value = (a: number, b: number) => a - b;
  setprevios(" - ");
}
</script>

<template>
  <div
    class="
      max-w-md
      mt-10
      h-[696px]
      bg-black
      mx-auto
      overflow-hidden
      relative
      bg-opacity-80
      shadow-xl shadow-gray-600/60
    "
  >
    <div
      :class="{ hidden: showSideMune && showhistory }"
      @click="hideMuneHistoy"
      class="bg-black absoute h-[696px] absolute w-[448px] bg-opacity-25"
    ></div>
    <div
      :class="{ '-translate-x-80': showSideMune }"
      class="
        h-[678px]
        mt-5
        transition
        absolute
        flex flex-col
        space-y-1
        w-80
        bg-zinc-900
      "
    >
      <button class="px-4" @click="showMune">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-7 w-7 mt-1 cursor-pointer text-white"
          viewBox="0 0 20 20"
          fill="currentColor"
        >
          <path
            fill-rule="evenodd"
            d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z"
            clip-rule="evenodd"
          />
        </svg>
      </button>
      <div class="h-[600px] flex flex-col py-10">
        <p class="font-semibold px-2 py-2 text-xl text-zinc-100">Calculator</p>
        <div class="flex items-center space-x-2 px-3 hover:bg-zinc-800">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6 text-zinc-100"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z"
            />
          </svg>
          <p class="py-2 text-xl text-zinc-100">Standard</p>
        </div>
        <div class="flex items-center hover:bg-zinc-800 space-x-2 px-3">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="text-zinc-100 h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"
            />
          </svg>
          <p class="py-2 text-xl text-zinc-100">Scientific</p>
        </div>
        <div  class="flex items-center space-x-2 px-3">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="text-zinc-100 h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M16 8v8m-4-5v5m-4-2v2m-2 4h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"
            />
          </svg>
          <p class=" py-2 text-xl text-zinc-100">
            Graphing
          </p>
        </div>
        <div>
          <p class="hover:bg-zinc-800 px-4 py-2 text-xl text-zinc-100">
            Programmer
          </p>
        </div>
        <div class="flex items-center space-x-2 px-3">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="text-zinc-100 h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
            />
          </svg>
          <p class="py-2 text-xl text-zinc-100">Date Calculation</p>
        </div>
        <div>
          <p class="px-2 font-semibold py-2 text-xl text-zinc-100">Convartar</p>
        </div>
        <div>
          <p class="hover:bg-zinc-800 px-4 py-2 text-xl text-zinc-100">
            Calculator
          </p>
        </div>
      </div>
      <div class="flex items-center text-zinc-200 space-x-2 px-4">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
          />
        </svg>
        <h1>About</h1>
      </div>
    </div>
    <div
      class="flex text-2xl font-semibold justify-between items-center px-4 pt-5"
    >
      <div class="flex space-x-3 text-2xl font-semibold items-center">
        <button @click="showMune">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-7 w-7 text-white"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path
              fill-rule="evenodd"
              d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z"
              clip-rule="evenodd"
            />
          </svg>
        </button>
        <h1 class="text-white">Standard</h1>
      </div>
      <div>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          @click="showHistory"
          class="text-white h-7 w-7 cursor-pointer"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"
          />
        </svg>
      </div>
    </div>
    <h1 class="text-xl text-neutral-500 font-semibold text-right mt-40 px-3">
      {{ watch || "." }}
    </h1>
    <div
      :class="{ 'translate-y-96': showhistory }"
      class="w-[448px] bg-zinc-900 h-[384px] bottom-0 absolute transition"
    >
      <div class="overflow-y-auto h-[340px] bg-zinc-900">
        <div
          v-for="each in history"
          class="text-right mt-5 hover:bg-zinc-800 transition px-4 snap-start"
        >
          <p class="text-zinc-400 font-semibold">{{ each.number }}</p>
          <h1 class="text-4xl text-white">{{ each.result }}</h1>
        </div>
        <h1 v-if="history.length === 0 + 1 || history.length === 0" class="text-lg text-zinc-300 px-4">
          There's no history yet
        </h1>
      </div>
      <svg @click="delet" xmlns="http://www.w3.org/2000/svg" class=" text-zinc-100 float-right mx-3 h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
</svg>
    </div>

    <div class="grid px-2 grid-cols-4 gap-1 pt-">
      <div class="text-white col-span-4 text-right pb-5 px-3 text-5xl">
        {{ number || "0" }}
      </div>
      <div @click="clear" class="button2">C</div>
      <div @click="percentage" class="button2">%</div>
      <div @click="remove" class="button2 flex justify-center">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M12 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2M3 12l6.414 6.414a2 2 0 001.414.586H19a2 2 0 002-2V7a2 2 0 00-2-2h-8.172a2 2 0 00-1.414.586L3 12z"
          />
        </svg>
      </div>
      <div @click="divide" class="button2">/</div>
      <div @click="action('7')" class="button">7</div>
      <div @click="action('8')" class="button">8</div>
      <div @click="action('9')" class="button">9</div>
      <div @click="multiply" class="button2">x</div>
      <div @click="action('4')" class="button">4</div>
      <div @click="action('5')" class="button">5</div>
      <div @click="action('6')" class="button">6</div>
      <div @click="mines" class="button2">-</div>
      <div @click="action('1')" class="button">1</div>
      <div @click="action('2')" class="button">2</div>
      <div @click="action('3')" class="button">3</div>
      <div @click="plus" class="button2">+</div>
      <div @click="action('0')" class="button col-span-2">0</div>
      <div @click="dot" class="button">.</div>
      <div @click="equal" class="button2">=</div>
    </div>
  </div>
</template>
