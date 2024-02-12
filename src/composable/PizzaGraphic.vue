<template>
    <div>
      <canvas ref="chartCanvas"></canvas>
    </div>
  </template>
  
  <script>
  import Chart from 'chart.js/auto'
  
  export default {
    props: {
      data: {
        type: Array,
        required: true
      }
    },
    mounted() {
      this.renderChart()
    },
    methods: {
      renderChart() {
        const ctx = this.$refs.chartCanvas.getContext('2d')
  
        new Chart(ctx, {
          type: 'doughnut',
          data: {
            labels: this.data.map(item => item.estado),
            datasets: [{
              label: 'Percentage',
              data: this.data.map(item => item.percentage.toFixed(2)),
                            backgroundColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(104,0,0,1)',
                'rgba(177,17,22,1)',
                'rgba(255,0,0,1)',
                'rgba(139,3,4,1)',
              ],
              borderWidth: 1
            }]
          },
          options: {
            responsive: true,
            maintainAspectRatio: false
          }
        })
      }
    }
  }
  </script>
