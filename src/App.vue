<template lang="html">
<div>

 <h1>Energy Mix UK</h1>

 <form v-on:submit.prevent="getTimeData">
   <label for="time-from">Time From</label>
    <input type="date" name="time-from" v-model="selectTimeFrom">
  <label for="time-from">Time From</label>
    <input type="date" name="time-to" v-model="selectTimeTo">
   <button type="submit" name="button">Find</button>
 </form>

 <generation-chart :chartData="dataFormatChart"></generation-chart>

 <generation-time-chart v-if="selectTimeData" :selectChartData="selectTimeData"></generation-time-chart>

</div>
</template>

<script>
import GenerationChart from './components/GenerationChart.vue';
import GenerationTimeChart from './components/GenerationTimeChart.vue';

export default {
  name: 'app',
  data(){
    return {
      chartData: [],
      timeFrom: "",
      timeTo:"",
      selectTimeFrom: "",
      selectTimeTo: "",
      selectTimeData: null
    }
  },
  mounted(){
    fetch('https://api.carbonintensity.org.uk/generation')
    .then(res => res.json())
    .then(data => {
      this.chartData = data.data.generationmix;
      this.timeFrom = data.data.from;
      this.timeTo = data.data.to;
    })
  },
  components: {
    'generation-chart': GenerationChart,
    'generation-time-chart': GenerationTimeChart
  },
  computed: {
    dataFormatChart(){
      let formattedData = [['fuel', 'percentage']]
      for (let fuel of this.chartData) {
        let entry = [fuel.fuel, fuel.perc]
        formattedData.push(entry)
      }
      return formattedData
    }
  },
  methods: {
    getTimeData(){
      fetch(`https://api.carbonintensity.org.uk/generation/${this.selectTimeFrom}/${this.selectTimeTo}`)
      .then(res => res.json())
      .then(data => {
        console.log('data', data.data)

        let headerData = ['Time']

        for (let fuel of data.data[0].generationmix) {
          headerData.push(fuel.fuel)
        }


        let formattedData = [headerData]

        for (let entry of data.data) {
          let entryLine = [entry.from]
          for (let fuel of entry.generationmix) {
            entryLine.push(fuel.perc)
          }
          formattedData.push(entryLine)
        }

        this.selectTimeData = formattedData
        }
        )
      }
  }

}
</script>

<style lang="css" scoped>
</style>
