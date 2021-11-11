<template>
  <v-dialog v-model="dialog">
    <template v-slot:activator="{ on, attrs }">
      <v-btn block color="info" dark v-bind="attrs" v-on="on">
        INGRESAR IDEA DE MEJORA
      </v-btn>
    </template>
    <v-card style="padding: 20px">
      <v-card-title> Registro de Idea de Mejora </v-card-title>
      <div style="margin: 0 1.5rem">
        <v-form ref="form" v-model="valid">
          <v-container>
            <!-- Propositor -->
            <v-row>
              <v-col cols="12" sm="6" md="4"
                ><v-text-field
                  v-model="emisor"
                  label="Emisor"
                  :rules="[(v) => !!v || 'Campo requerido.']"
                  required
                ></v-text-field
              ></v-col>
              <v-col cols="12" sm="6" md="4"
                ><v-text-field
                  v-model="depto"
                  label="Departamento"
                  :rules="[(v) => !!v || 'Campo requerido.']"
                  required
                ></v-text-field
              ></v-col>
              <v-col cols="12" md="4"
                ><v-text-field
                  v-model="areaPropone"
                  label="Área de quien propone"
                  :rules="[(v) => !!v || 'Campo requerido.']"
                  required
                ></v-text-field
              ></v-col>
            </v-row>
            <v-row>
              <v-col cols="12" md="6"
                ><v-text-field
                  v-model="supervisorPropone"
                  label="Supervisor de quien propone"
                  :rules="[(v) => !!v || 'Campo requerido.']"
                  required
                ></v-text-field
              ></v-col>
              <v-col cols="12" md="6"
                ><v-text-field
                  v-model="gerentePropone"
                  label="Gerente de quien propone"
                  :rules="[(v) => !!v || 'Campo requerido.']"
                  required
                ></v-text-field
              ></v-col>
            </v-row>
            <v-row>
              <v-col
                ><v-text-field
                  v-model="areaOportunidad"
                  label="Área de oportunidad de mejora"
                  :rules="[(v) => !!v || 'Campo requerido.']"
                  required
                ></v-text-field
              ></v-col>
            </v-row>
            <v-row>
              <v-col cols="12" md="6"
                ><v-text-field
                  v-model="supervisorArea"
                  label="Supervisor del área de mejora"
                  :rules="[(v) => !!v || 'Campo requerido.']"
                  required
                ></v-text-field
              ></v-col>
              <v-col cols="12" md="6"
                ><v-text-field
                  v-model="gerenteArea"
                  label="Gerente del Área de mejora"
                  :rules="[(v) => !!v || 'Campo requerido.']"
                  required
                ></v-text-field
              ></v-col>
            </v-row>
            <v-row
              ><v-col>
                <v-text-field
                  v-model="titulo"
                  label="Título de la propuesta"
                  :rules="[(v) => !!v || 'Campo requerido.']"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row
              ><v-col
                ><v-text-field
                  v-model="oportunidad"
                  label="Oportunidad de mejora"
                  :rules="[(v) => !!v || 'Campo requerido.']"
                  required
                ></v-text-field></v-col
            ></v-row>
            <v-row
              ><v-col
                ><v-text-field
                  v-model="propuesta"
                  label="Propuesta de mejora"
                  :rules="[(v) => !!v || 'Campo requerido.']"
                  required
                ></v-text-field></v-col
            ></v-row>
            <v-row>
              <v-col>
                <template>
                  <v-file-input
                    accept="image/*"
                    label="Foto antes"
                    prepend-icon="mdi-camera"
                  ></v-file-input>
                </template>
              </v-col>
            </v-row>
            <v-row justify="center">
              <v-col cols="auto">
                <v-btn color="error" @click="cancel()">CANCELAR</v-btn>
              </v-col>
              <v-col cols="auto">
                <v-btn
                  color="success"
                  :loading="loading"
                  :disabled="loading"
                  @click="check()"
                  >GUARDAR</v-btn
                >
              </v-col>
            </v-row>
          </v-container>
        </v-form>
      </div>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data() {
    return {
      loader: null,
      loading: false,

      valid: false,

      emisor: "",
      depto: "",
      areaPropone: "",
      supervisorPropone: "",
      gerentePropone: "",
      areaOportunidad: "",
      supervisorArea: "",
      gerenteArea: "",
      titulo: "",
      oportunidad: "",
      propuesta: "",

      dialog: false,
    };
  },

  methods: {
    check() {
      this.validate();
      if (this.valid) {
        this.loader = "loading";
        this.send();
      }
    },
    validate() {
      this.$refs.form.validate();
    },
    send() {
      var data = {
        idEmpleado: this.emisor,
        titulo: this.titulo,
        areaOportunidad: this.areaOportunidad,
        oportunidad: this.oportunidad,
        propuesta: this.propuesta,
        imgAntes: "string", //url a cdn de imágenes
      };
      fetch("https://localhost:5001/api/data/addMejora2", {
        method: "POST",
        mode: "no-cors",
        body: JSON.stringify(data),
        headers: {
        "Content-Type": "application/json;",
      },
      }).then(() => {
        alert("Idea registrada exitosamente.");
      });

      this.clearForm();
      this.dialog = false;
    },
    cancel() {
      this.clearForm();
      this.dialog = false;
    },
    clearForm() {
      this.emisor = "";
      this.depto = "";
      this.areaPropone = "";
      this.supervisorPropone = "";
      this.gerentePropone = "";
      this.areaOportunidad = "";
      this.supervisorArea = "";
      this.gerenteArea = "";
      this.titulo = "";
      this.oportunidad = "";
      this.propuesta = "";
    },
  },

  watch: {
    loader() {
      const l = this.loader;
      this[l] = !this[l];

      setTimeout(() => (this[l] = false), 3000);

      this.loader = null;
    },
  },
};
</script>

<style scoped>
h2 {
  text-align: center;
}
</style>
