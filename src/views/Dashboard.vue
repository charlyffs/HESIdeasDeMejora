<template>
  <div>
    <v-data-table
      style="margin: 2rem"
      :headers="headers"
      :items="items"
      class="elevation-1"
      pagination.sync="pagination"
      item-key="id"
      loading="true"
      @click:row="loadReport"
    >
    </v-data-table>
  </div>
</template>

<script>
import axios from "axios";
import { headers } from "../config/headers.ts";
export default {
  data() {
    return {
      headers: [
        {
          text: "# Propuesta",
          align: "start",
          value: "numProp",
        },
        { text: "Mes", value: "mes" },
        { text: "Fecha Propuesta", value: "fecha" },
        { text: "Área de quien propone", value: "areaPropone" },
        { text: "Título", value: "titulo" },
        { text: "Área de mejora", value: "areaMejora" },
        { text: "Tipo de mejora", value: "tipoMejora" },
        { text: "Gerente", value: "gerente" },
      ],
      items: [
        {
          numProp: "1",
          mes: "text",
          fecha: "text",
          areaPropone: "text",
          titulo: "text",
          areaMejora: "text",
          tipoMejora: "text",
          gerente: "text",
        },
        {
          numProp: "2",
          mes: "text",
          fecha: "text",
          areaPropone: "text",
          titulo: "text",
          areaMejora: "text",
          tipoMejora: "text",
          gerente: "text",
        },
      ],
    };
  },
  methods: {
    loadReport(row) {
      this.$router.push("/reporte/" + row.numProp);
    },
  },
  async mounted() {
    const response = await axios.get(
      "https://localhost:5001/api/data/dashboard",
      {
        method: "GET",
        headers: headers,
      }
    );
    console.log("Server response: ", response.data);
    this.items = response.data;
  },
};
</script>

<style></style>
