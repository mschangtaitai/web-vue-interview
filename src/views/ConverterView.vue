<template>
  <div class="px-6  py-10 sm:py-14">
    <div class="mx-auto max-w-2xl text-center">
      <h2 class="text-4xl font-bold tracking-tight text-gray-900 sm:text-6xl">Currency converter</h2>
      <p class="mt-6 text-lg leading-8 text-gray-600">Convert one currency into another selecting from the selection
        options and entering an amount.</p>
    </div>
  </div>
  <!-- Implement a UI that would behave like a currency converter -->
  <div>
    <div class="font-bold">From</div>
    <select v-model="from">
      <option v-for="currency in currencies" :value="currency.code">
        {{ currency.code }} - {{ currency.name }}
      </option>
    </select>
    <div class="font-bold">To</div>
    <select v-model="to">
      <option v-for="currency in currencies" :value="currency.code">
        {{ currency.code }} - {{ currency.name }}
      </option>
    </select>
    <div class="font-bold">Date:</div>
    <input type="date" v-model="date" />

    <div class="font-bold">Amount:</div>
    <input v-model="amount" id="amount" name="amount"
      class="block w-full rounded-md border-0 bg-white py-1.5 pl-10 pr-3 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
      placeholder="Amount" type="number" />
    <button @click="convert" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Convert</button>
    <div v-if="result">
      <div>Conversion rate: {{ result.info.rate }}</div>
      <div>Result: {{ result.result }}</div>
    </div>
  </div>
</template>
<script setup>
import { computed, onMounted, reactive, ref } from "vue";

import useAxios from "@/composables/useAxios.js"

const axios = useAxios()


// TODO implement the logic to convert by calling the correct endpoint for more information check: https://fxratesapi.com/docs/endpoints/convert-currency
const from = ref(null)
const to = ref(null)
const date = ref(new Date().toISOString().substring(0, 10))
const amount = ref()
const result = ref(null)

const currencies = reactive([])

const getCurrencies = onMounted(async () => {
  try {
    const response = await axios.get("/currencies")
    const data = response.data
    // console.log(data)
    for (const currency in data) {
      currencies.push(data[currency]);
    }
    //TODO This line contains an error fix it to show all the cards
    // currencies.push(...data)
  } catch (error) {

  }
})

function convert() {
  const options = {
    "method": "GET",
    "url": "https://api.fxratesapi.com/convert?from=" + from.value + "&to=" + to.value + "&date=" + date.value + "&amount=" + amount.value + "&format=json"
  };

  axios.request(options).then(function (response) {
    result.value = response.data;
  }).catch(function (error) {
    console.error(error);
  });
} 
</script>