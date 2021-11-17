<template>
  <div>
    <v-container>
      <v-row justify="center">
        <v-col cols="12" sm="8">
          <VerticalBarChart v-bind:inputData="verticalBarData" />
        </v-col>
        <v-col cols="12" sm="4"
          ><PieChart v-bind:inputData="pieChartData"
        /></v-col>
      </v-row>
      <v-row justify="center">
        <v-col
          ><HorizontalBarChart v-bind:inputData="horizontalBarData"
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
      verticalBarData: [
        //mes y total de ideas
        ["ENE", 2],
        ["ENE", 2],
      ],
      pieChartData: [
        ["Propuestas", 25],
        ["Por proponer", 25],
      ],
      horizontalBarData: [
        //Nombre de empleado y num de ideas
        ["JOHN DOE", 10],
        ["JOHN DOE", 10],
      ],
    };
  },
  mounted() {
    fetch("http://charlyffs.mywire.org:8001/indicatorsHori", {
      method: "GET",
      headers: {
        "Content-Type": "application/json;",
        "Access-Control-Allow-Origin": "*",
      },
    })
      .then((response) => response.json())
      .then((data) => (this.horizontalBarData = data));

    fetch("http://charlyffs.mywire.org:8001/indicatorsVer", {
      method: "GET",
      headers: {
        "Content-Type": "application/json;",
        "Access-Control-Allow-Origin": "*",
      },
    })
      .then((response) => response.json())
      .then((data) => (this.verticalBarData = data));

    fetch("http://charlyffs.mywire.org:8001/indicatorsPie", {
      method: "GET",
      headers: {
        "Content-Type": "application/json;",
        "Access-Control-Allow-Origin": "*",
      },
    })
      .then((response) => response.json())
      .then((data) => (this.pieChartData = data));

    this.verticalBarData.unshift(["Mes", "Ideas"]);
    this.pieChartData.unshift(["Tipo", "Progreso"]);
    this.horizontalBarData.unshift(["Nombre", "Avance"]);

    console.log(this.verticalBarData);
    console.log(this.pieChartData);
    console.log(this.horizontalBarData);
  },
};
</script>

<style></style>
