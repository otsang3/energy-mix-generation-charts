<template lang="html">
  <div>
    <GChart
      type="LineChart"
      :data="selectChartData"
      :options="chartOptions"
    />
    <!-- <p>{{chartData}}</p> -->
  </div>
</template>

<script>
import { GChart } from 'vue-google-charts'

export default {
  name: 'generation-time-chart',
  data(){
    return {
      chartOptions: {

          'title': 'Energy UK Mix',
          'subtitle': 'Sales, Expenses, and Profit: 2014-2017',
          'height': 400,

      }
    }
  },
  props: ['selectChartData'],
  components: {
    GChart
  }
}
</script>

<style lang="css" scoped>
</style>
