<!-- comentarios generales
    - al cargar la pantalla se ocupan:
            - los datos de la idea propuesta
    - el botón cerrar abre un cuadro de confirmación (no estoy segura de a dónde debe regresar)
    - el botón aprobación abre un cuadro de diálogo donde habrán las opciones Aprobar y Rechazar
        - el botón Aceptar dentro del cuadro de diálogo de Aprobación hará un método POST porque debe guardar si la idea se aprobó o rechazó 
        y mandar a la 2da aprobación en caso de que sea aprobada
    
 -->

<template>
  <v-container>
    <v-row>
      <v-col>
        <h2>SISTEMA DE IDEAS DE MEJORA</h2>
        <h3>Primera aprobación</h3>
      </v-col>
    </v-row>
    <v-row>
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
            <v-card>
                <v-card-title class="text-h5 grey lighten-2">
                    Cerrar propuesta
                </v-card-title>

                <div id="propuestaFactible">
                <h3 class="ma-4">¿Desea cerrar esta propuesta?</h3>
                <v-card-actions>
                    <v-row>
                        <v-col>
                            <v-btn block color="blue" class="ma-2 pa-2 white--text">
                                CANCELAR
                            </v-btn>
                        </v-col>
                        <v-col>
                            <v-btn block color="blue" class="ma-2 pa-2 white--text" to="/">
                                ACEPTAR
                            </v-btn>
                        </v-col>
                    </v-row>
                </v-card-actions>
                </div>
            </v-card>

        </v-dialog>
        |
        </p>
        <v-dialog v-model="dialogAprobacion" width="500">
            <template v-slot:activator="{ on, attrs }">
                <v-btn x-small plain v-bind="attrs" v-on="on">
                    Aprobación
                </v-btn>
            </template>

            <v-card>
                <v-card-title class="text-h5 grey lighten-2">
                    Aprobación
                </v-card-title>

                <div id="aprobarRechazar">
                <v-card-actions>
                    <v-radio-group v-model="primeraAprobacion" row class="ma-2">
                        <v-radio label="Aprobar" value="aprobar"></v-radio>
                        <v-radio label="Rechazar" value="rechazar"></v-radio>
                    </v-radio-group>
                </v-card-actions>
                    
                    <div v-if="primeraAprobacion == 'aprobar'">
                        <v-card-actions>
                            <v-row>
                                <v-col>
                                    <v-select v-model="tipoMejora" :items="tipoMejoraItems" label="Tipo de mejora" class="ma-2"></v-select>
                                </v-col>
                            </v-row>
                        </v-card-actions>
                    </div>
                    <div v-else>
                        <v-card-actions>
                            <v-row>
                                <v-select v-model="rechazoJustificacion" :items="rechazoJustificacionItems" label="Justificación" class="ma-2"></v-select>
                            </v-row>
                        </v-card-actions>

                        <v-card-actions>
                            <v-row>
                                <v-text-field v-model="rechazoComentarios" label="Comentarios" value="" solo class="ma-2"></v-text-field>
                            </v-row>
                        </v-card-actions>
                    </div>


                <v-card-actions>
                        <v-row>
                            <v-col>
                                <v-btn block color="blue" class="ma-2 white--text" @click="dialogAprobacion = false">
                                    CANCELAR
                                </v-btn>
                            </v-col>
                            <v-col>
                                <v-btn block color="blue" class="ma-2 white--text" @click="aceptar()">
                                    ACEPTAR
                                </v-btn>
                            </v-col>
                        </v-row>
                    </v-card-actions>
                </div>
            </v-card>
        </v-dialog>
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
        dialogAprobacion: false,
        dialogCerrar: false,
        tipoMejoraItems: ['Movimientos', 'Inventario', 'Proceso / Organización', 'Sobreproducción', 'Tiempo', 'Calidad: Defectos/Retrabajos', 'Esperas', 'Costos / Ahorros', 'Medio ambiente / Energía'],
        rechazoJustificacionItems: ['Existe un proyecto relacionado con la mejora', 'No es viable por inversión', 'No es idea, es corrección', 'No es idea, es necesidad'],
        primeraAprobacion: "aprobar",
        propuestaMejora: "",
        opMejora: "",
        imgAntes: "",
        nombreDepto: "",
        tituloPropuesta: "",
        tipoMejora: "",
        nombreSupervisor: "",
        areaMejora: "",
        nombreGnte: "",
        fecha: "",
        areaPropone: "",
        nombreEmisor: "",
        numPropuesta: "",
        rechazoComentarios: "",
        rechazoJustificacion: null,
        aprobar: null,
        rechazar: null,
    }),
    methods:
    {
        aceptar()
        {
            // método post
            // se necesita: 
        },
        cancelar()
        {
            this.dialogAprobacion = false;
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

