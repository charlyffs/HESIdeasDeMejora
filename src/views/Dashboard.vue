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
        { text: "# Aprobación", value: "aprobacion" },
        { text: "Estatus", value: "estatus" },
      ],
      items: [
        {
          numProp: "No hay datos",
          mes: "",
          fecha: "",
          areaPropone: "",
          titulo: "",
          areaMejora: "",
          tipoMejora: "",
          gerente: "",
          estatus: ""
        },
      ],
    };
  },
  methods: {
    loadReport(row) {
      this.$router.push("/approval1/" + row.numProp);
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
    if(response.data.length > 0) this.items = response.data;

    // const approval1 = await axios.get(
    //   "https://localhost:5001/api/data/getAprobacion1",
    //   {
    //     method: "GET",
    //     headers: headers,
    //   }
    // );
    // const approval2 = await axios.get(
    //   "https://localhost:5001/api/data/getAprobacion2",
    //   {
    //     method: "GET",
    //     headers: headers,
    //   }
    // );

  },
};
</script>

<style>

</style>
