<template>
  <div>
    <v-container grid-list-xs>
      <v-row>
        <v-col cols="12">
          <h4>MEJORES IDEAS DEL MES</h4>
        </v-col>
      </v-row>
      <v-row justify="space-around">
        <!-- Podium, 3 of the below cols -->
        <ProjectCard :items="firstPlace" />
        <ProjectCard :items="secondPlace" />
        <ProjectCard :items="thirdPlace" />
      </v-row>
    </v-container>
    <div style="height: 40px"></div>
    <h4>PARTICIPACION</h4>
    <div style="height: 20px"></div>
    <v-data-table
      style="margin: 0 2rem"
      :headers="tableHeaders"
      :items="tableData"
      class="elevation-1"
      pagination.sync="pagination"
      item-key="id"
      loading="true"
    >
    </v-data-table>
  </div>
</template>

<script>
import ProjectCard from "@/components/ProjectCard.vue";
import axios from "axios";
export default {
  components: { ProjectCard },
  data() {
    return {
      tableHeaders: [
        {
          text: "# Prop",
          align: "start",
          value: "numProp",
        },
        { text: "Nombre", value: "nombre" },
        { text: "Área de quien propone", value: "areaPropone" },
        { text: "Título de la propuesta", value: "titulo" },
      ],
      tableData: [
        { numProp: "123", nombre: "asdf", areaPropone: "asdf", titulo: "asdf" },
      ],
      firstPlace: {
        place: "1",
        title: "test",
        author: "author",
        description: "description",
      },
      secondPlace: {
        place: "2",
        title: "test",
        author: "author",
        description: "description",
      },
      thirdPlace: {
        place: "3",
        title: "test",
        author: "author",
        description: "description",
      },
    };
  },
  mounted() {
    console.log(axios);
    axios.get("url").then((res) => (this.firstPlace = res));
    axios.get("url").then((res) => (this.secondPlace = res));
    axios.get("url").then((res) => (this.thirdPlace = res));
    axios.get("url").then((res) => (this.tableData = res));
  },
};
</script>

<style scoped>
h3,
h4,
p {
  text-align: center;
}
</style>
