<template lang="html">
  <div>
    <GChart
      type="LineChart"
      :data="chartData"
      :options="chartOptions"
    />
    <p>{{chartData}}</p>
  </div>
</template>

<script>
import { GChart } from 'vue-google-charts'

export default {
  name: 'generation-vue',
  data(){
    return {
      chartOptions: {

          title: 'Energy UK Mix',
          subtitle: 'Sales, Expenses, and Profit: 2014-2017'

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
