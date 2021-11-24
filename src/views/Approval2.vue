<!-- comentarios generales
    - al cargar la pantalla se ocupan:
                - los datos de la idea propuesta
    - falta que propuesta factible se pinte de verde y propuesta no factible de naranja
    - los botones Propuesta factible y Propuesta no factible abren cuadros de diálogo
        - el botón Aceptar en ambos cuadros de diálogo hacen un método POST para guardar si la idea fue aprobada por segunda ocasión o si se rechazó
    

 -->


<template>
  <v-container>
    <v-row>
      <v-col>
        <h2>SISTEMA DE IDEAS DE MEJORA</h2>
        <h3>Segunda aprobación - Aprobación técnica (Supervisor / Ingeniería)</h3>
      </v-col>
    </v-row>
    <v-row justify="left">
      <div class = "inicio">
         <p>INFORMACIÓN GENERAL <span id = "icon">PENDIENTE DE REVISIÓN (HES)</span></p>
      </div>
    </v-row>

    <v-row> 
        <p>
        <v-dialog v-model="dialogCerrar" width="500">       
            <template v-slot:activator="{ on, attrs }">
                <v-btn x-small plain v-bind="attrs" v-on="on">
                    Cerrar
                </v-btn>
            </template>



        </v-dialog>
        |
        <v-dialog v-model="dialogPropuestaFactible" width="500">       
            <template v-slot:activator="{ on, attrs }">
                <v-btn x-small plain v-bind="attrs" v-on="on">
                    Propuesta factible
                </v-btn>
            </template>

            <v-card>
                <v-card-title class="text-h5 grey lighten-2">
                    Finalizar propuesta
                </v-card-title>

                <div id="propuestaFactible">
                    <h3 class="ma-4">¿Es factible realizar esta propuesta de mejora?</h3>
                        <v-card-actions>
                            <v-row>
                                <v-col>
                                    <v-btn block color="blue" class="white--text" @click="dialogPropuestaFactible = false">
                                        CANCELAR
                                    </v-btn>
                                </v-col>
                                <v-col>
                                    <v-btn block color="blue" class="white--text">
                                        ACEPTAR
                                    </v-btn>
                                </v-col>
                            </v-row>
                        </v-card-actions>
                    </div>
            </v-card>
        </v-dialog>
        |
        <v-dialog v-model="dialogPropuestaNoFactible" width="500">       
            <template v-slot:activator="{ on, attrs }">
                <v-btn x-small plain v-bind="attrs" v-on="on">
                    Propuesta no factible
                </v-btn>
            </template>

            <v-card>
                <v-card-title class="text-h5 grey lighten-2">
                    Propuesta no factible
                </v-card-title>

                <div id="aprobarRechazar">
                <v-card-actions>
                    <v-row>
                        <v-select class="pa-4" :items="noFactJustificacionItems" label="Justificación"></v-select>
                    </v-row>
                </v-card-actions>
                    <v-row>
                        <v-textarea name="noFactComentarios" class="pa-8" label="Comentarios" value="" solo auto-grow></v-textarea>
                    </v-row>
                <v-card-actions>
                    <v-row>
                        <v-col>
                            <v-btn block color="blue" class="pa--4 ma--4 white--text" @click="dialogPropuestaNoFactible = false">
                                CANCELAR
                            </v-btn>
                        </v-col>
                        <v-col>
                            <v-btn block color="blue" class="pa--4 ma--4 white--text">
                                ACEPTAR
                            </v-btn>
                        </v-col>
                    </v-row>
                </v-card-actions>
                </div>
            </v-card>
        </v-dialog>
        </p>
    </v-row>

    <div class="infogeneral">
        <v-row>
            <v-col>
                <v-text name="hola"># Propuesta</v-text>
            </v-col>
            <v-col>
                <v-text>Propuesta por</v-text>
            </v-col>
            <v-col>
                <v-text>UAP/DEPTO</v-text>
            </v-col>
            <v-col>
                <v-text>Área de quien propone</v-text>
            </v-col>
            <v-col>
                <v-text>Fecha</v-text>
            </v-col>
        </v-row>    
        <v-row>
            <v-col>
                <v-text v-model="numPropuesta">21-001</v-text>
            </v-col>
            <v-col>
                <v-text v-model="nombreEmisor">JESÚS CARRILLO</v-text> 
            </v-col>
            <v-col>
                <v-text v-model="nombreDepto">HES</v-text>
            </v-col>
            <v-col>
                <v-text v-model="areaPropone">HES</v-text>
            </v-col>
            <v-col>
                <v-text v-model="fecha">04/08/2021</v-text>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
                <v-text>Gnte. de quien</v-text>
            </v-col>
            <v-col>
                <v-text>Área de la Mejora</v-text>
            </v-col>
            <v-col>
                <v-text>Supervisor del área de mejora</v-text>
            </v-col>
            <v-col>
                <v-text>Tipo de Mejora</v-text>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
                <v-text v-model="nombreGnte">JESÚS CARRILLO</v-text>
            </v-col>
            <v-col>
                <v-text v-model="areaMejora">Almacén</v-text>
            </v-col>
            <v-col>
                <v-text v-model="nombreSupervisor">AARON MANRIQUEZ</v-text>
            </v-col>
            <v-col>
                <v-text v-model="tipoMejora">Movimientos</v-text>
            </v-col>
        </v-row>
        </div>

        <v-divider class="ma-8"></v-divider>

        <div class="datosidea">
        <v-row>
            <v-col>
                <p>Título de la propuesta</p>
                <v-text-field v-model="tituloPropuesta" value="Hola" solo readonly></v-text-field>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
                <p>Oportunidad de mejora</p>
                <v-text-field v-model="opMejora" value="" solo readonly></v-text-field>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
                <p>(Antes)</p>
                <v-img v-model="imgAntes" max-height="100%" max-width="100%" src="../assets/prueba.png" aspect-ratio="1.7"></v-img>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
                <p>Propuesta de mejora</p>
                <v-textarea v-model="propuestaMejora" value="" readonly solo auto-grow></v-textarea>
            </v-col>
        </v-row>
    </div>
        <template>
            <v-row>
                <v-col>
                    <v-btn block color="blue" class="ma-2 white--text">Guardar</v-btn>
                </v-col>
                <v-col>
                    <v-btn block color="blue" class="ma-2 white--text">Finalizar</v-btn>
                </v-col>
            </v-row>
        </template>
  </v-container>
</template>

<script>
export default {
    data: () => ({
      dialogPropuestaNoFactible: false,
      dialogPropuestaFactible: false,
      noFactJustificacionItems: ['No es viable por riesgo de seguridad', 'No es viable, incumple especificaciones de proceso', 'No es viable, riesgo de calidad', 'No es viable, falta de tecnología'],
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
.inicio #icon{
    color: #339CFF;
}
.infogeneral p{
    margin: 0 auto;
}
</style>

