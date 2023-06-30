<template>
  <q-page class="flex flex-start items-center column">
    <q-toolbar
      class="card justify-center items-center rounded-borders q-gutter-x-md q-mt-md q-ma-sm q-pa-sm col-3 col-lg-6"
      style="min-height: 10rem; max-height: fit-content; width: 99%;">
      <div class="row justify-center q-gutter-y-sm q-gutter-x-sm">
        <q-card flat bordered class="flex column justify-center col-3 col-lg-1"
          style="overflow: auto; min-height: 8rem; max-height: 8rem; padding-left: 30px; padding-right: 30px; min-width: 190px;">
          <q-card-main class="cardMain flex justify-center text-h4">
            15
          </q-card-main>
          <q-card-title class="cardTitle flex justify-center text-subtitle2 text-accent">
            Total Atendimentos
          </q-card-title>
        </q-card>
        <q-card flat bordered class="flex column justify-center col-3 col-lg-1"
          style="overflow: auto; min-height: 8rem; max-height: 8rem; padding-left: 30px; padding-right: 30px;  min-width: 190px;">
          <q-card-main class="cardMain flex justify-center text-h4">
            1
          </q-card-main>
          <q-card-title class="cardTitle flex justify-center text-subtitle2 text-accent">
            Receptivos
          </q-card-title>
        </q-card>
        <q-card flat bordered class="flex column justify-center col-3 col-lg-1"
          style="overflow: auto; min-height: 8rem; max-height: 8rem; padding-left: 30px; padding-right: 30px;  min-width: 190px;">
          <q-card-main class="cardMain flex justify-center text-h4">
            9
          </q-card-main>
          <q-card-title class="cardTitle flex justify-center text-subtitle2 text-accent">
            Ativos
          </q-card-title>
        </q-card>
        <q-card flat bordered class="flex column justify-center col-3 col-lg-1"
          style="overflow: auto; min-height: 8rem; max-height: 8rem; padding-left: 30px; padding-right: 30px;  min-width: 190px;">
          <q-card-main class="cardMain flex justify-center text-h4">
            2142
          </q-card-main>
          <q-card-title class="cardTitle flex justify-center text-subtitle2 text-accent">
            Atendimentos
          </q-card-title>
        </q-card>
        <q-card flat bordered class="flex column justify-center col-3 col-lg-2"
          style="overflow: auto; min-height: 8rem; max-height: 8rem; padding-left: 30px; padding-right: 30px;  min-width: 300px;">
          <q-card-main class="cardMain flex justify-center text-h5">
            3 minutos
          </q-card-main>
          <q-card-title class="cardTitle flex justify-center text-subtitle2 text-accent">
            Tempo Médio de Atendimento (TMA)
          </q-card-title>
        </q-card>
        <q-card flat bordered class="flex column justify-center col-3 col-lg-2"
          style="overflow: auto; min-height: 8rem; max-height: 8rem; padding-left: 30px; padding-right: 30px;  min-width: 300px;">
          <q-card-main class="cardMain flex justify-center text-h5">
            8 segundos
          </q-card-main>
          <q-card-title class="cardTitle flex justify-center text-subtitle2 text-accent">
            Tempo Médio 1ª Resposta
          </q-card-title>
        </q-card>

      </div>
    </q-toolbar>
    <div class="flex row q-gutter-x-lg full-width">
      <q-card flat class="card q-ma-sm col">
        <q-card-section class="q-pa-sm q-pa-sm-md">
          <VueApexCharts height="300" width="100%" type="donut" :options="chartOptions" :series="atendFila">
          </VueApexCharts>
        </q-card-section>
      </q-card>
      <q-card flat class="card q-ma-sm col">
        <q-card-section class="q-pa-sm q-pa-sm-md">
          <VueApexCharts height="300" width="100%" type="donut" :options="chartOptions2" :series="atendCanal">
          </VueApexCharts>
        </q-card-section>
      </q-card>
    </div>
    <div class="flex row q-gutter-x-lg full-width">
      <q-card flat class="card q-ma-sm col">
        <q-card-section class="q-pa-md">
          <VueApexCharts height="300" width="100%" type="bar" :options="chartOptions3" :series="chartOptions3.series">
          </VueApexCharts>
        </q-card-section>
      </q-card>
    </div>
    <div class="flex row q-gutter-x-lg full-width">
      <q-card flat class="card q-ma-sm col">
        <q-card-section class="q-pa-md">
          <VueApexCharts height="300" width="100%" type="line" :options="chartOptions4" :series="chartOptions4.series">
          </VueApexCharts>
        </q-card-section>
      </q-card>
    </div>
    <div class="flex row q-gutter-x-lg full-width">
      <q-card flat class="card q-ma-sm col">
        <q-card-section class="q-pa-md">
          <q-table flat bordered title="Performance Usuários" :rows="usuarios" :columns="columns" row-key="e-mail"
            color="amber" />
        </q-card-section>
      </q-card>
    </div>
  </q-page>
</template>

<style lang="scss" ></style>

<script setup>
import VueApexCharts from "vue3-apexcharts";
import { formatDuration } from 'date-fns'
import {
  usuarios,
  atendFila,
  atendCanal,
} from '../static/mock'


const chartOptions = {
  labels: ['Fila-1', 'Fila-2', 'Fila-3', 'Fila-4', 'Fila-5'],
  chart: {
    width: 380,
    type: 'donut',
    toolbar: {
      show: true,
    },
  },
  plotOptions: {
    pie: {
      startAngle: -90,
      endAngle: 270,
      customScale: 0.9,
    }
  },
  dataLabels: {
    enabled: true,
    style: {
      fontSize: '16px',
      offsetY: '150',
      fontFamily: 'Helvetica, Arial, sans-serif'
    },
    offsetX: 0
  },
  fill: {
    type: 'gradient',
  },
  legend: {
    position: 'bottom',
    formatter: function (val, opts) {
      return val + " - " + opts.w.globals.series[opts.seriesIndex]
    },
    labels: {
      colors: '#ee741b',
    },
  },
  title: {
    text: 'Atendimento por fila',
    style: {
      color: '#ee741b'
    },
  },
  theme: {
    palette: 'palette2'
  },

  responsive: [{
    breakpoint: 480,
    options: {
      chart: {
        width: 200
      },
    }
  }]
}
const chartOptions2 = {
  labels: ['Fila-1', 'Fila-2', 'Fila-3', 'Fila-4', 'Fila-5'],
  chart: {
    width: 380,
    type: 'donut',
    toolbar: {
      show: true,
    },
  },
  plotOptions: {
    pie: {
      startAngle: -90,
      endAngle: 270,
      customScale: 0.9,
    }
  },
  dataLabels: {
    enabled: true,
    style: {
      fontSize: '16px',
      offsetY: '150',
      fontFamily: 'Helvetica, Arial, sans-serif'
    },
    offsetX: 0
  },
  fill: {
    type: 'gradient',
  },
  legend: {
    position: 'bottom',
    formatter: function (val, opts) {
      return val + " - " + opts.w.globals.series[opts.seriesIndex]
    },
    labels: {
      colors: '#ee741b',
    },
  },
  title: {
    text: 'Atendimento por canal',
    style: {
      color: '#ee741b'
    },
  },
  responsive: [{
    breakpoint: 480,
    options: {
      chart: {
        width: 200
      },
      legend: {
        position: 'bottom'
      }
    }
  }]
}
const chartOptions3 = {
  chart: {
    type: 'bar'
  },
  series: [{
    name: 'Atendimentos',
    data: [30, 40, 45, 50, 49, 60]
  }],
  title: {
    text: 'Evolução por canal',
    style: {
      color: '#ee741b'
    },
  },
  yaxis: {
    title: {
      text: 'Atendimentos',
      style: {
        color: '#ee741b'
      }
    },
    labels: {
      style: {
        colors: '#ee741b'
      }
    },
  },
  xaxis: {
    categories: ["Jan", "Fev", "Mar", "Abr", "Mai", "Jun"],
    labels: {
      style: {
        colors: '#ee741b'
      }
    },
  },
  dataLabels: {
    style: {
      fontSize: '12px',
      fontWeight: 'bold',
    },
    dropShadow: {
      enabled: true,
      left: 2,
      top: 2,
      opacity: 0.5
    }
  },
  tooltip: {
    shared: false,
    fillSeriesColor: true,
    x: {
      show: false,
    },
  },
}
const chartOptions4 = {
  colors: ['#008FFB'],
  chart: {
    toolbar: {
      tools: {
        download: true,
        selection: false,
        zoom: false,
        zoomin: false,
        zoomout: false,
        pan: false,
        reset: false
      }
    }
  },
  series: [{
    name: 'Atendimentos',
    type: 'column',
    data: [30, 40, 45, 50, 49, 60]
  }, {
    name: 'Atendimentos',
    type: 'line',
    data: [30, 40, 45, 50, 49, 60]
  }],
  title: {
    text: 'Evolução atendimentos',
    style: {
      color: '#ee741b'
    },
  },
  yaxis: {
    title: {
      text: 'Atendimentos',
      style: {
        color: '#ee741b'
      }
    },
    labels: {
      style: {
        colors: '#ee741b'
      }
    },
  },
  xaxis: {
    categories: ["Jan", "Fev", "Mar", "Abr", "Mai", "Jun"],
    labels: {
      style: {
        colors: '#ee741b'
      }
    },
  },
  tooltip: {
    shared: false,
    fillSeriesColor: true,
    x: {
      show: false,
    },
  },
  dataLabels: {
    enabled: true,
    enabledOnSeries: [1],

    style: {
      fontSize: '12px',
      fontWeight: 'bold',
    },
    dropShadow: {
      enabled: true,
      left: 2,
      top: 2,
      opacity: 0.5
    }
  },
  legend: {
    show: false,
  },
}

const columns = [
  {
    name: 'name',
    required: true,
    label: 'Usuário',
    align: 'left',
    field: row => row.name,
    format: (v, r) => {
      r.email ? r.email : ''
      return v ? `${r.name} | ${r.email}` : 'Não informado'
    },
    sortable: true
  },
  { name: 'pendentes', label: 'Pendentes', field: 'pendentes', sortable: true },
  { name: 'atendendo', label: 'Atendendo', field: 'atendendo', sortable: true },
  { name: 'finalizados', label: 'Finalizados', field: 'finalizados', sortable: true },
  { name: 'total', label: 'Total', field: 'total', sortable: true },
  {
    name: 'tme', label: 'T.M.E', field: 'tme', align: 'center', sortable: true,
    format: v => {
      return formatDuration(v) || ''
    }
  },
  {
    name: 'tma', label: 'T.M.A ', field: 'tma', align: 'center', sortable: true,
    format: v => {
      return formatDuration(v) || ''
    }
  },
]




</script>
