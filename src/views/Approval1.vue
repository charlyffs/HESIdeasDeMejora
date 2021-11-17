<template>
  <v-container>
    <v-row>
      <v-col>
        <h2>SISTEMA DE IDEAS DE MEJORA</h2>
        <h3>Primera aprobación</h3>
      </v-col>
    </v-row>
    <v-row justify="left">
      <div class = "inicio">
         <p>INFORMACIÓN GENERAL <span id = "icon">PENDIENTE DE REVISIÓN (HES)</span></p>
      </div>
    </v-row>
    <v-row>
        <v-dialog
      v-model="dialog"
      width="500">
        <template v-slot:activator="{ on, attrs }">
        <p>
        <v-btn x-small plain>
            Cerrar
        </v-btn>
        |
        <v-btn x-small plain>
            Editar gral.
        </v-btn>
        |
        <v-btn x-small plain>
            Eliminar
        </v-btn>
        |
        <v-btn x-small plain v-bind="attrs" v-on="on">
            Aprobación
        </v-btn>
        </p>
        </template>

        <v-card>
        <v-card-title class="text-h5 grey lighten-2">
          Aprobación
        </v-card-title>

        <div id="aprobarRechazar">
        <v-card-actions>
            <v-radio-group v-model="primeraAprobacion" row>
                <v-radio label="Aprobar" value="aprobar"></v-radio>
                <v-radio label="Rechazar" value="rechazar"></v-radio>
            </v-radio-group>
        </v-card-actions>

        <v-card-actions>
            <v-col>
                <v-btn class="ma-2" block>
                    Cancelar
                </v-btn>
            </v-col>

            <v-col>
                <v-btn class="ma-2" block @click:>
                    Aceptar
                </v-btn>
            <p>radiobutton: {{ primeraAprobacion }}</p>
            </v-col>
        </v-card-actions>
        </div>
        </v-card>
        </v-dialog>
      </v-row>
    
    <div class="infogeneral">
        <v-row>
            <v-col>
                <p align="center"># Propuesta</p>
                <p align="center">21-001</p>
            </v-col>
            <v-col>
                <p align="center">Propuesta por</p>
                <p align="center">JESÚS CARRILLO</p> 
            </v-col>
            <v-col>
                <p align="center">UAP/DEPTO</p>
                <p align="center">HES</p>
            </v-col>
            <v-col>
                <p align="center">Área de quien propone</p>
                <p align="center">HES</p>
            </v-col>
            <v-col>
                <p align="center">Fecha</p>
                <p align="center">04/08/2021</p>
            </v-col>
        </v-row>    
        <v-row>
            <v-col>
                <p align="center">Gnte. de quien</p>
                <p align="center">JESÚS CARRILLO</p>
            </v-col>
            <v-col>
                <p align="center">Área de la Mejora</p>
                <p align="center">Almacén</p>
            </v-col>
            <v-col>
                <p align="center">Supervisor del área de mejora</p>
                <p align="center">AARON MANRIQUEZ</p>
            </v-col>
            <v-col>
                <p align="center">Tipo de Mejora</p>
                <p align="center">Movimientos</p>
            </v-col>
        </v-row>
        </div>

        <v-divider class="ma-8"></v-divider>

        <div class="datosidea">
        <v-row>
            <v-col>
                <p>Título de la propuesta</p>
                <v-text-field value="" solo disabled></v-text-field>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
                <p>Oportunidad de mejora</p>
                <v-text-field value="" solo disabled></v-text-field>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
                <p>(Antes)</p>
                <v-img max-height="100%" max-width="100%" src="" aspect-ratio="1.7"></v-img>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
                <p>Propuesta de mejora</p>
                <v-textarea name="input-7-1" value="" disabled solo auto-grow hint="Hint text"></v-textarea>
            </v-col>
        </v-row>
        </div>
        <template>
            <v-row>
                <v-col class="ma-2">
                    <v-btn block color="blue" class="white--text">Guardar</v-btn>
                </v-col>
                <v-col>
                    <v-btn block color="blue" class="white--text">Finalizar</v-btn>
                </v-col>
            </v-row>
        </template>
  </v-container>
</template>

<script>
    export default {
    data () {
      return {
        primeraAprobacion: null,
      }
    }
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
.inicio #icon{
    color: #339CFF;
}
.infogeneral p{
    margin: 0 auto;
}
</style>

