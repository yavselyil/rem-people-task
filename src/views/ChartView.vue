<template>
  <div class="chart-view">
    <div class="navbar">
      <p class="header">Competitor Comparative Product Availability</p>
    </div>
    <highcharts
      :options="chartOptions"
      :constructor-type="'chart'"
    ></highcharts>
    <button class="log-out-btn" @click="logOut()">Log Out!</button>
  </div>
</template>

<script>
import Highcharts from "highcharts";
import Vue from "vue";
import HighchartsVue from "highcharts-vue";
import jsonChartData from "../drilldown-column-chart";
import { Chart } from "highcharts-vue";
import exportingInit from "highcharts/modules/exporting";
import loadDrillDown from "highcharts/modules/drilldown";
exportingInit(Highcharts);

loadDrillDown(Highcharts);
Vue.use(HighchartsVue, { Highcharts });

export default {
  components: {
    highcharts: Chart
  },
  data() {
    return {
      chartOptions: {
        chart: {
          type: "column"
        },
        title: {
          text: "Products"
        },
        xAxis: {
          type: "category"
        },
        legend: {
          enabled: false
        },
        plotOptions: {
          series: {
            borderWidth: 0,
            dataLabels: {
              enabled: true
            }
          }
        },
        series: [
          {
            name: "Products",
            colorByPoint: true,
            data: jsonChartData.series[0].data
          }
        ],
        drilldown: {
          series: jsonChartData.data
        }
      }
    };
  },
  beforeCreate: function() {
    document.body.className = "chart";
  },
  methods: {
    logOut() {
      this.$router.push("/");
      this.$noty.success("Successfully logged out!");
    }
  }
};
</script>

<style>
.log-out-btn {
  position: absolute;
  top: 35px;
  right: 50px;
  font-weight: bold;
  font-size: 13px;
  color: #fff;
  background-color: #e93890;
  border-color: #ff69b4;
  border-radius: 6px;
  -webkit-box-shadow: 0px 0px 10px 3px rgba(255, 105, 180, 0.88);
  -moz-box-shadow: 0px 0px 10px 3px rgba(255, 105, 180, 0.88);
  box-shadow: 0px 0px 10px 3px rgba(255, 105, 180, 0.88);
  height: 25px;
}

.chart-view .navbar {
  border: 2px solid rgba(60, 58, 58, 0.5);
  max-width: 100%;
  background: rgba(60, 58, 58, 0.5);
  text-align: left;
  padding-left: 50px;
}

.header {
  color: white;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  font-size: 24px;
}
</style>
