<template>
  <div>
    <v-container>
      <v-row justify="center">
        <v-col cols="12" sm="8"
          ><VerticalBarChart v-bind:inputData="unnamedChartData"
        /></v-col>
        <v-col cols="12" sm="4"
          ><PieChart v-bind:inputData="globalGoalProgress"
        /></v-col>
      </v-row>
      <v-row justify="center">
        <v-col
          ><HorizontalBarChart v-bind:inputData="employeeGoalProgress"
        /></v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import HorizontalBarChart from "@/components/HorizontalBarChart.vue";
import VerticalBarChart from "@/components/VerticalBarChart.vue";
import PieChart from "@/components/PieChart.vue";
import axios from "axios";

export default {
  name: "Indicators",
  components: {
    HorizontalBarChart,
    VerticalBarChart,
    PieChart,
  },
  data() {
    return {
      unnamedChartData: [
        ["ENE", 2],
        ["ENE", 2],
      ],
      globalGoalProgress: [
        ["1", 25],
        ["1", 25],
      ],
      employeeGoalProgress: [
        ["JOHN DOE", 10],
        ["JOHN DOE", 10],
      ],
    };
  },
  mounted() {
    axios.get("url").then((res) => (this.unnamedChartData = res));
    axios.get("url").then((res) => (this.globalGoalProgress = res));
    axios.get("url").then((res) => (this.employeeGoalProgress = res));
    this.unnamedChartData.unshift(["Mes", "Ideas"]);
    this.globalGoalProgress.unshift(["Task", "Hours per Day"]);
    this.employeeGoalProgress.unshift(["Nombre", "Avance"]);
  },
};
</script>

<style></style>
