<template>
  <v-container>
    <v-row>
      <v-col>
        <v-btn color="info">Ver propuesta</v-btn>
        <h2>SISTEMA DE IDEAS DE MEJORA</h2>
        <h3>Acciones de mejora</h3>
      </v-col>
    </v-row>
    <v-row justify="left">
      <div class = "inicio">
         <p>RESPONSABLES Y ACCIONES</p>
      </div>
    </v-row>

    <v-row> 
      <v-select class="pa-4" width="5%" :items="items" label="Seleccionar piloto"></v-select> 
      <v-select class="pa-4" width="5%" :items="items2" label="Indicador de mejora"></v-select> 
      <v-text-field label="Indicador inicial" value=""></v-text-field>
      <v-select class="pa-4" width="5%" :items="items3" label="U/M"></v-select>
    </v-row>

    <v-divider class="pa-4"></v-divider>

    <div class="ma-4 acciones">
        <v-row>
            <v-row>
            <v-card
    class="mx-auto" max-width="100%"
  >

    <v-list two-line>
      <v-list-item-group
        v-model="selected"
        active-class="blue--text"
      >
        <template v-for="(item, index) in items4">
          <v-list-item :key="item.title">
            <template>
              <v-list-item-content>
                <v-list-item-title v-text="item.title"></v-list-item-title>

                <v-list-item-subtitle
                  class="text--primary"
                  v-text="item.headline"
                ></v-list-item-subtitle>

                <v-list-item-subtitle v-text="item.subtitle"></v-list-item-subtitle>
              </v-list-item-content>

              <v-list-item-action>
                <v-list-item-action-text v-text="item.action"></v-list-item-action-text>
              </v-list-item-action>
            </template>
          </v-list-item>

          <v-divider
            v-if="index < items4.length - 1"
            :key="index"
          ></v-divider>
        </template>
      </v-list-item-group>
    </v-list>
  </v-card>

        </v-row>

            <v-dialog
            v-model="dialog"
            width="500">       
                <template v-slot:activator="{ on, attrs }">
                    <v-btn block color="blue" class="ma-8 white--text" v-bind="attrs" v-on="on" justify="right">Agregar acción</v-btn>
                </template>

                <v-card>
                    <v-card-title class="text-h5 grey lighten-2">
                        Agregar acción
                    </v-card-title>

                    <v-card-actions>
                        <v-row>
                            <v-text-field class="ma-4" label="Acción a realizar" value=""></v-text-field>
                        </v-row>
                    </v-card-actions>

                    <v-card-actions>
                        <v-row>
                            <v-text-field class="ma-4" label="Descripción" value=""></v-text-field>
                        </v-row>
                    </v-card-actions>

                    <v-card-actions>
                        <v-row>
                            <v-col>
                                <v-btn block color="blue" class="pa-4 white--text" @click="dialog = false">
                                    CANCELAR
                                </v-btn>
                            </v-col>
                            <v-col>
                                <v-btn block color="blue" class="white--text" @click="dialog = false">
                                    ACEPTAR
                                </v-btn>
                            </v-col>
                        </v-row>
                    </v-card-actions>
                </v-card>
            </v-dialog>
        </v-row>
    </div>

    <v-row>
        <v-col>
            <p class="resultados">(Después)</p>
            <v-file-input
            label="Cargar imagen"
            filled
            prepend-icon="mdi-camera" class="ma-4"></v-file-input>
        </v-col>
    </v-row>

    <v-row>
        <v-col>
            <p class="resultados">Resultados</p>
            <v-row>
                <v-col>
                    <p>Indicador de mejora</p>
                    <v-text-field value="Cantidad de piezas" solo readonly></v-text-field>
                </v-col>

                <v-col>
                    <p>Indicador inicial</p>
                    <v-text-field value="45" solo readonly></v-text-field>
                </v-col>

                <v-col>
                    <p>Indicador final</p>
                    <v-text-field value="15" solo readonly></v-text-field>
                </v-col>

                <v-col>
                    <p>U/M</p>
                    <v-text-field value="QTY" solo readonly></v-text-field>
                </v-col>

                <v-col>
                    <p>Mejora obtenida</p>
                    <v-text-field value="33%" solo readonly></v-text-field>
                </v-col>
            </v-row>
        </v-col>
    </v-row>

    <v-divider class="ma-4"></v-divider>

    <v-row>
        <v-col>
            <p class="resultados">Estándar actualizado</p>
            <v-row>
                <v-col>
                    <p>Nombre</p>
                    <v-text-field value="" solo></v-text-field>
                </v-col>

                <v-col>
                    <p>Nomenclatura</p>
                    <v-text-field value="" solo></v-text-field>
                </v-col>
            </v-row>
        </v-col>
    </v-row>

    <v-row>
        <v-col>
            <v-btn block color="blue" class="pa-4 white--text">GUARDAR</v-btn>
        </v-col>
        <v-col>
            <v-btn block color="blue" class="pa-4 white--text">FINALIZAR</v-btn>
        </v-col>
    </v-row>
        
  </v-container>
</template>

<script>
export default {
    data: () => ({
      items: ['Nombre1', 'Nombre2', 'Nombre3', 'Nombre4'], 
      items2: ['Cantidad de piezas', 'Tiempo de espera', 'Tiempo de ciclo', 'Mano de obra', '% Eficiencia', 'Tiempo muerto', 'Piso utilizado', 'Inventarios', 'Equipo utilizado', 'Desperdicio de material', 'Partes y refacciones', 'Retrabajos', 'Flujo / Transportación', 'Rechazos internos', 'Rechazos externos'], 
      items3: ['MIN', 'QTY', '%', 'M/2', '$', 'M', 'PZS'],
      dialog: false,
      items4: [
        {
          action: 'xxxxxxxxxxxx',
          headline: 'Acción',
          subtitle: `Descripción`,
          title: 'Piloto/Responsable',
        },
        {
          action: 'xxxxxxxxxxxx',
          headline: 'Acción',
          subtitle: `Descripción`,
        },
      ],
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
