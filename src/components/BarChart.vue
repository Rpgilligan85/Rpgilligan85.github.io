<template>
  <v-layout row>
    <v-flex>
      <highcharts :options="chartOptions()" ref="highcharts"></highcharts>
    </v-flex>
  </v-layout>
</template>

<script>
import { mapState, mapActions } from "vuex";
const d3 = require("d3");

export default {
  name: "BarChart",
  data() {
    return {
      chartReady: false
    };
  },
  computed: {
    ...mapState(["chartType", "chartData", "headers", "selectedHeader"]),
    ...mapActions(["addChartOptions"])
  },
  methods: {
    chartOptions: function() {
      return {
        chart: {
          type: this.chartType
        },
        title: {
          text: this.selectedHeader
        },
        xAxis: {
          categories: this.headers
        },
        series: this.chartData
      };
    }
  },
  watch: {},
  mounted() {
    console.log(this.chartOptions);
    this.$store.dispatch("addChartOptions", this.chartOptions());
  }
};
</script>

<style lang="scss">
</style>
