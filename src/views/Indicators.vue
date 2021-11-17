<template>
  <div>
    <v-container>
      <v-row justify="center">
        <v-col cols="12" sm="8">
          <VerticalBarChart v-bind:inputData="unnamedChartData" />
        </v-col>
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
        //mes y total de ideas
        ["ENE", 2],
        ["ENE", 2],
      ],
      globalGoalProgress: [
        ["Propuestas", 25],
        ["Por proponer", 25],
      ],
      employeeGoalProgress: [
        //Nombre de empleado y num de ideas
        ["JOHN DOE", 10],
        ["JOHN DOE", 10],
      ],
    };
  },
  mounted() {
    fetch("DATA", {
      method: "GET",
      mode: "no-cors",
      headers: {
        "Content-Type": "application/json;",
      },
    }).then((response) => (this.unnamedChartData = response));
    fetch("DATA", {
      method: "GET",
      mode: "no-cors",
      headers: {
        "Content-Type": "application/json;",
      },
    }).then((response) => (this.globalGoalProgress = response));
    fetch("DATA", {
      method: "GET",
      mode: "no-cors",
      headers: {
        "Content-Type": "application/json;",
      },
    }).then((response) => (this.employeeGoalProgress = response));
    this.unnamedChartData.unshift(["Mes", "Ideas"]);
    this.globalGoalProgress.unshift(["Task", "Hours per Day"]);
    this.employeeGoalProgress.unshift(["Nombre", "Avance"]);
  },
};
</script>

<style></style>
