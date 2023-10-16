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
    <div>TO IMPLEMENT :D we got to show the rate and the amount in the new currency</div>
    <div>(Optional) also add a custom date option default is now</div>
    <div class="flex flex-row items-center justify-around">
      <div class="font-bold">You can take the following image as base</div>
      <img class="h-[556px]"
        src="https://mir-s3-cdn-cf.behance.net/projects/404/2b3f91152882841.Y3JvcCwxNjMwLDEyNzQsMCwxMg.png" />
    </div>

  </div>
</template>
<script setup>
import { ref } from 'vue';

// TODO implement the logic to convert by calling the correct endpoint for more information check: https://fxratesapi.com/docs/endpoints/convert-currency
const from = ref(null)
const to = ref(null)
const date = ref(null)
const amount = ref(null)
</script>