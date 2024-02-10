<template>
  <div class="h-96 w-auto bg-light-red border-4 border-solid border-secundary rounded-md flex justify-center">
    <div class="flex flex-col items-center p-2">
      <h1 class="font-bold text-3xl flex justify-center pt-4 mb-16">
        Estados participantes:
      </h1>
      <div class="flex flex-row justify-center items-center p-2">
        <SpButton @click="handleButtonClick('São Paulo')" />
        <RjButton @click="handleButtonClick('Rio de Janeiro')" />
        <MgButton @click="handleButtonClick('Minas Gerais')" />
        <EsButton @click="handleButtonClick('Espírito Santo')" />
        <OthersButton @click="handleButtonClick('Outros Estados')" />
      </div>
      <div class="flex flex-row justify-center items-center font-medium text-2xl p-4">
        <h3>{{ resultMessage }}</h3>
      </div>
    </div>
  </div>
</template>

<script setup>
  import { ref } from 'vue'
  import SpButton from '@/components/globals/buttons/SpButoon.vue'
  import EsButton from '@/components/globals/buttons/EsButton.vue'
  import MgButton from '@/components/globals/buttons/MgButton.vue'
  import OthersButton from '@/components/globals/buttons/OthersButton.vue'
  import RjButton from '@/components/globals/buttons/RjButton.vue'
  import data from '../data/data.json'

  const activeButton = ref(null)
  const resultMessage = ref('')
  const totalValue = ref(0)

  data.forEach(item => {
    totalValue.value += item.valor
  })

  const handleButtonClick = (button) => {
    activeButton.value = button

    const selectedState = data.find(item => item.estado === button)

    if (selectedState) {
      resultMessage.value = `${selectedState.estado} tem um valor de R$ ${selectedState.valor.toFixed(2)}
      de um total de R$ ${totalValue.value.toFixed(2)}`
    }
  }
</script>
