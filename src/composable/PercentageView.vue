<template>
  <div class="h-96 w-auto bg-light-red border-4 border-solid border-secundary rounded-md flex justify-center">
    <div class="bg-light-red flex justify-center p-4">
      <PizzaGraphic :data="chartData" />
    </div>
    <div class="flex flex-col items-center p-2">
      <h1 class="font-bold text-3xl flex justify-center pt-4 mb-16">
        Estados participantes:
      </h1>
      <div class="flex flex-row justify-center items-center p-2">
        <SpButton @click="handleButtonClick('São Paulo')" />
        <RjButton @click="handleButtonClick('Rio de Janeiro')" />
        <MgButton @click="handleButtonClick('Minas Gerais')" />
        <EsButton @click="handleButtonClick('Espírito Santo')" />
        <OthersButton @click="handleButtonClick('Outros')" />
      </div>
      <div class="flex flex-row justify-center items-center font-medium text-2xl p-4">
        <h3>{{ resultMessage }}</h3>
      </div>
      <div class="flex flex-row justify-center items-center font-medium text-2xl p-4">
        <h3>{{ percentage }}</h3>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import data from '../data/data.json'
import PizzaGraphic from '@/composable/PizzaGraphic.vue'
import SpButton from '@/components/globals/buttons/SpButoon.vue'
import EsButton from '@/components/globals/buttons/EsButton.vue'
import MgButton from '@/components/globals/buttons/MgButton.vue'
import RjButton from '@/components/globals/buttons/RjButton.vue'
import OthersButton from '@/components/globals/buttons/OthersButton.vue'

export default {
  components: {
    SpButton,
    RjButton,
    MgButton,
    EsButton,
    OthersButton,
    PizzaGraphic
  },
  setup() {
    const activeButton = ref(null)
    const resultMessage = ref('')
    const percentage = ref('')
    const totalValue = data.reduce((acc, curr) => acc + curr.valor, 0)
    const chartData = data.map(item => ({
      estado: item.estado,
      percentage: (item.valor / totalValue) * 100
    }))

    const handleButtonClick = (button) => {
      activeButton.value = button

      const selectedState = data.find(item => item.estado === button)

      if (selectedState) {
        const percentageValue = (selectedState.valor / totalValue) * 100
        percentage.value = percentageValue.toFixed(2) + '%'
        resultMessage.value = `${selectedState.estado} tem um valor de R$ ${selectedState.valor.toFixed(2)} do total de R$ ${totalValue.toFixed(2)}`
      }
    }

    return {
      resultMessage,
      percentage,
      chartData,
      handleButtonClick
    }
  }
}
</script>
