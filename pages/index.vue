<template>
  <v-container class="my-container" style="max-width: 100%;">
    <v-row style="min-height: 90vh;">
      <v-col cols="8" class="flex-grow-1 flex-shrink-1" >
        <client-only>
          <ECharts ref="chart" :options="options_leaflet" theme="theme" autoresize />
        </client-only>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import ECharts from 'vue-echarts'
import 'echarts'
// import 'echarts-leaflet'
export default {
  components: {
    ECharts,
  },
  mounted() {
    require('echarts-leaflet') // needs to be imported client-side
  },
  data() {
    return {
      options: {
        xAxis: {
          type: 'category',
          data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
        },
        yAxis: {
          type: 'value'
        },
        series: [{
          data: [820, 932, 901, 934, 1290, 1330, 1320],
          type: 'line'
        }]
      },
      options_leaflet: {
        leaflet: {
          center: [120.13066322374, 30.240018034923],
          zoom: 3,
          roam: true,
          tiles: [{
            label: 'OpenStreetMap',
            urlTemplate: 'https://{s}.tile.openstreetmap.fr/hot/{z}/{x}/{y}.png',
            options: {
              attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>, Tiles courtesy of <a href="http://hot.openstreetmap.org/" target="_blank">Humanitarian OpenStreetMap Team</a>'
            }
          }]
        },
        series: [{
          coordinateSystem: 'leaflet',
          type: 'scatter',
        }]
      },
    }
  },
}
</script>
<style>
.echarts {
  width: 100%;
  height: 100%;
}
</style>
