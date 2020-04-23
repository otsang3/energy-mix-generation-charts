<template lang="html">
 <h1>Enery Mix UK</h1>
</template>

<script>
export default {
  name: 'app',
  data(){
    return {
      chartData: [],
      timeFrom: "",
      timeTo:""
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
  }

}
</script>

<style lang="css" scoped>
</style>
