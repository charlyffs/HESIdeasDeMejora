<!-- comentarios generales
    - falta botón Ver propuesta
    - el botón Guardar va a hacer un método POST porque estos datos se ocuparán en la pantalla Tasks
    - el botón Cerrar no estoy segura de a dónde tiene que regresar
 -->

<template>
  <v-container>
    <v-row>
      <v-col>
        <v-btn color="info" @click="verPropuesta()">Ver propuesta</v-btn>
        <h2>SISTEMA DE IDEAS DE MEJORA</h2>
        <h3>Asignar piloto</h3>
      </v-col>
    </v-row>
    <v-row>
      <div class = "inicio">
         <p>RESPONSABLES Y ACCIONES</p>
      </div>
    </v-row>

    <v-row> 
      <v-select v-model="seleccionarPiloto" class="pa-4" width="5%" :items="seleccionarPilotoSelect" label="Seleccionar piloto"></v-select> 
      <v-select v-model="indicadorMejora" class="pa-4" width="5%" :items="indicadorMejoraSelect" label="Indicador de mejora"></v-select> 
      <v-text-field v-model="indicadorInicial" label="Indicador inicial" value=""></v-text-field>
      <v-select v-model="unidadMedida" class="pa-4" width="5%" :items="unidadMedidaSelect" label="U/M"></v-select>
    </v-row>

    <v-row>
        <v-col>
            <v-btn block color="blue" class="pa-4 white--text" @click="cerrar">CERRAR</v-btn>
        </v-col>
        <v-col>
            <v-btn block color="blue" class="pa-4 white--text" @click="guardar" to="/">GUARDAR</v-btn>
        </v-col>
    </v-row>
        
  </v-container>
</template>

<script>
export default {
  data: () => ({
    seleccionarPilotoSelect: ['Nombre1', 'Nombre2', 'Nombre3', 'Nombre4'],
    indicadorMejoraSelect: ['Cantidad de piezas', 'Tiempo de espera', 'Tiempo de ciclo', 'Mano de obra', '% Eficiencia', 'Tiempo muerto', 'Piso utilizado', 'Inventarios', 'Equipo utilizado', 'Desperdicio de material', 'Partes y refacciones', 'Retrabajos', 'Flujo / Transportación', 'Rechazos internos', 'Rechazos externos'], 
    unidadMedidaSelect: ['MIN', 'QTY', '%', 'M/2', '$', 'M', 'PZS'],
    dialog: false,
  }),
}
</script>

<style>
h3 {
  text-align: center;
}
h2 {
  text-align: center;
}
.inicio{
    font-weight: bold;
}
.resultados{
    font-weight: bold;
}
.infogeneral p{
    margin: 0 auto;
}
</style>
