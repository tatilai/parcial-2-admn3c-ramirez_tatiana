<template>
  <v-form>
    <v-container>
      <v-row>
        <v-col cols="12" sm="6" md="3">
          <v-text-field v-model="nombreProyecto" label="Nombre del proyecto"></v-text-field>
        </v-col>
        <v-col cols="12" sm="6" md="3">
          <v-text-field v-model="responsable" label="Responsable"></v-text-field>
        </v-col>
        <v-col cols="12" md="6">
          <v-container fluid>
            <v-textarea v-model="descripcion" autocomplete="explicacion del proyecto" label="Descripción"></v-textarea>
          </v-container>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
export default {
  name: 'Formulario',
  data() {
    return {
      nombreProyecto: '',
      responsable: '',
      descripcion: '',
    };
  },
};
</script>