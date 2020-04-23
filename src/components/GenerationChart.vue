<template lang="html">
  <div>
    <GChart
      type="PieChart"
      :data="chartData"
      :options="chartOptions"
    />
  </div>
</template>

<script>
import { GChart } from 'vue-google-charts'

export default {
  name: 'generation-vue',
  data(){
    return {
      chartOptions: {

          'title': 'Energy UK Mix',
          'subtitle': 'Sales, Expenses, and Profit: 2014-2017',
          'height': 400

      }
    }
  },
  props: ['chartData'],
  components: {
    GChart
  }
}
</script>

<style lang="css" scoped>
</style>
