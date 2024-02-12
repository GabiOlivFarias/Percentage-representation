<template>
  <div class="relative md:m-8 m-4 min-h-screen md:min-w-full bg-light-red border-4 border-solid border-secundary rounded-md md:p-7 p-4 flex flex-col justify-center items-center">
    <img class="hidden lg:block absolute top-0 right-0 w-40 px-4 mt-4 mr-4" src="../public/images/logo.png" />
    <div class="md:pb-24 pb-12">
      <h1 class="flex justify-center font-bold md:text-4xl text-2xl">
        {{ $t('tittle') }}
      </h1>
    </div>
    <PercentageView />
  </div>
</template>

<script setup>
import PercentageView from './composable/PercentageView.vue'

</script>
