<template>
  <div class="md:m-8 min-h-screen md:min-w-full bg-light-red md:border-4 md:border-solid md:border-secundary rounded-md md:p-7 flex flex-col justify-center items-center">
    <div class="md:pb-12 pb-6">
      <h1 class="font-bold text-2xl md:text-4xl flex justify-center pt-4 mb-8">
        {{ $t('subtittle') }}
      </h1>

      <div class="flex flex-col md:flex-row justify-center items-center p-2 md:space-x-4">
        <SpButton @click="handleButtonClick('São Paulo')" />
        <RjButton @click="handleButtonClick('Rio de Janeiro')" />
        <MgButton @click="handleButtonClick('Minas Gerais')" />
        <EsButton @click="handleButtonClick('Espírito Santo')" />
        <OthersButton @click="handleButtonClick('Outros')" />
      </div>
      
      <div class="flex flex-col items-center p-2">
        <h3 class="font-medium text-xl">{{ resultMessage }}</h3>
        <h3 class="font-medium text-xl">{{ percentage }}</h3>
      </div>
    </div>

    <div class="bg-light-red flex justify-center md:p-4">
      <PizzaGraphic :data="chartData" />
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
