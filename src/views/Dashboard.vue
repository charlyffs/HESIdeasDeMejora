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
  mounted() {
    fetch("http://charlyffs.mywire.org:8001/dashboard", {
      method: "GET",
      headers: {
        "Content-Type": "application/json;",
        "Access-Control-Allow-Origin": "*",
      },
    })
      .then((response) => response.json())
      .then((data) => (this.items = data));
  },
};
</script>

<style></style>
