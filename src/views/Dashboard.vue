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
          numProp: "lorem ipsum",
          mes: "lorem ipsum",
          fecha: "lorem ipsum",
          areaPropone: "lorem ipsum",
          titulo: "lorem ipsum",
          areaMejora: "lorem ipsum",
          tipoMejora: "lorem ipsum",
          gerente: "lorem ipsum",
        },
      ],
    };
  },
  async mounted() {
    const response = await axios.get("https://localhost:5001/api/data/awards", { 
        method: "GET",
        headers: headers,
      })
    console.log("Server response: ",response.data);
    this.items = response.data;
    },
};
</script>

<style></style>
