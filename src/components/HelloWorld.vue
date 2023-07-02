<!--<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>-->


<template>
  <div>
    <span>Equipo 1</span>
    <v-text-field
      v-model="nombre"
      :counter="10"
      :rules="reglasNombre"
      label="Nombre del proyecto"
      required
    ></v-text-field>

    <v-text-field
      v-model="responsable"
      :rules="reglasResponsable"
      label="Responsable"
      required
    ></v-text-field>

    <v-container fluid>
      <v-textarea
        autocomplete="descripcion"
        label="Descripcion del proyecto"
      ></v-textarea>
    </v-container>

     <v-btn
      :disabled="!valid"
      color="#FFE082"
      class="mr-4"
      @click="validate"
    >
     Continuar
    </v-btn>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>