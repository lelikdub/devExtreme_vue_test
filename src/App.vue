<template>
  <v-app id="app">
    <v-main>
      <v-row>
        <v-col>
          <v-btn
              color="primary"
              @click="showDialog"
          >
            создать график
          </v-btn>
        </v-col>
      </v-row>
      <new-chart-dialog
          :show="showNewChartDialog"
          @close="showNewChartDialog=false"
          @newChart="addChart"
      />
      <v-row v-for="(item, index) in charts" :key="'chart-' + index">
        <pie-chart v-if="item.chartType===1" :chart-data="item.chartData" />
        <line-chart v-else :chart-data="item.chartData" />
      </v-row>
    </v-main>
  </v-app>
</template>

<script>
import NewChartDialog from './components/newChartDialog'
import pieChart from './components/pieChart'
import lineChart from './components/lineChart'

export default {
  name: 'App',
  components: {
    NewChartDialog,
    pieChart,
    lineChart,
  },
  data () {
    return {
      showNewChartDialog: false,
      charts: [],
    }
  },
  methods: {
    addChart (val) {
      this.showNewChartDialog = false
      this.charts.unshift(val)
    },
    showDialog () {
      this.showNewChartDialog = true
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
