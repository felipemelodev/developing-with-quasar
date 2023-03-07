<template>
  <q-page>
    <div class="row flex-center q-pt-xl q-pb-xl">
      <q-card flat bordered class="my-card col-8 q-mb-xl">
      <q-card-section>
        <div class="text-h6">Média de público nos estádios 2023</div>
      </q-card-section>

      <q-card-section class="q-pt-none">
        <apexchart
          type="bar"
          height="350"
          :options="chartOptions"
          :series="series"
        >
      </apexchart>
      </q-card-section>

      </q-card>
      <q-card flat bordered class="my-card col-8">
      <q-card-section>
        <div class="text-h6">Média de público nos estádios 2023</div>
      </q-card-section>

      <q-card-section class="q-pt-none">
        <apexchart
          type="bar"
          height="350"
          :options="chartOptions"
          :series="series"
        >
      </apexchart>
      </q-card-section>

      </q-card>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'IndexPage',
  data () {
    return {
      series: [{
        name: 'Flamengo',
        data: [39, 35, 50, 37, 30, 25, 27, 39, 42],
        color: '#e31d12'
      },
      {
        name: 'Corinthians',
        data: [40, 42, 45, 37, 39, 43, 41, 47, 49],
        color: '#000'
      },
      {
        name: 'Palmeiras',
        data: [35, 30, 22, 26, 33, 15, 27, 36, 12],
        color: '#19ba11'
      }],
      chartOptions: {
        chart: {
          type: 'bar',
          height: 350
        },
        plotOptions: {
          bar: {
            horizontal: false,
            columnWidth: '55%',
            endingShape: 'rounded'
          }
        },
        dataLabels: {
          enabled: false
        },
        stroke: {
          show: true,
          width: 2,
          colors: ['transparent']
        },
        xaxis: {
          categories: ['Fev', 'Mar', 'Abr', 'Mai', 'Jun', 'Jul', 'Ago', 'Set', 'Out']
        },
        yaxis: {
          title: {
            text: '(mil torcedores)'
          }
        },
        fill: {
          opacity: 1
        },
        tooltip: {
          y: {
            formatter: function (val) {
              return val + '.000 torcedores'
            }
          }
        }
      }
    }
  }
})
</script>
