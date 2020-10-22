<template>
  <section id="chart-section">
        <div class="chart-buttons">
            <button v-on:click="bakePie('0'); changeChartType('PieChart');">Pie Chart</button>
            <button v-on:click="changeChartType('BarChart')">Bar Chart</button>
            <button v-on:click="changeChartType('ColumnChart')">Column Chart</button>
            <button v-on:click="bakePie('0.4'); changeChartType('PieChart');">Donut Chart</button>
        </div>
        <GChart v-if="energyDetails" :type="chartType" :data="energyDetails" :options="chartOptions"/>
  </section>
</template>

<script>
import { GChart } from "vue-google-charts"

export default {
    name: 'generate-chart',
    props: ['energyDetails'],
    
    data() {
        return {
            chartOptions: {
                title: 'Energy Generation Mix',
                subtitle: '30 minute energy usage',
                width: '75%',
                height: '500',
                hAxis: {
                    title: "Fuel Type"
                },
                vAxis: {
                    title: "Percentage (%)",
                    minValue: 0,
                    maxValue: 100
                },
                pieHole: 0
            },
            chartType: 'ColumnChart',
        }
    },
    methods: {
        changeChartType: function(chartName) {
            this.chartType = chartName
        },
        bakePie: function(holeSize) {
            this.chartOptions.pieHole = holeSize;
        }
    },
    components: {
        GChart
    }
}
</script>

<style lang="css" scoped>
</style>