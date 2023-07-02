<!--<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>-->


<template>
  <div>
     <p class="font-weight-bold w-400 display-1 text-center my-4">
      Equipo 1
    </p>
   <v-img
  :src="require('@/assets/equipo_1.png')"
   max-height="205"
   max-width="205"
   blur="0"
   class="mx-auto"
   id="imagenUno"
  ></v-img>

<div class="formularioUno"> 
  <v-form  
   ref="form"
   v-model="valid"
   lazy-validation>
     <v-text-field
      v-model="name"
      :rules="nameRules"      
      label="Nombre del proyecto"
      required     
    ></v-text-field>
    <v-text-field
      v-model="email"
      :rules="emailRules"
      label="Responsable"
      required      
    ></v-text-field>

    <v-container fluid>
      <v-textarea
      v-model="description"
       :rules="descriptionRules"        
       label="Descripcion del proyecto"
      ></v-textarea>
    </v-container>

     <v-btn
      class="mr-4"
      @click="continuarProyecto"
      color="#FFE082">
      Continuar
    </v-btn>
   
    </v-form>
    
    </div>



   
  </div>
</template>

<script>
export default {
  data() {
    return {
      valid: false,
      name: '',
      email: '',
      description: '',
      nameRules: [
        (v) => !!v || 'El nombre del proyecto es requerido',
        (v) => (v && v.length <= 10) || 'El nombre del proyecto debe tener máximo 10 caracteres',
      ],
      emailRules: [
        (v) => !!v || 'El responsable es requerido',
      ],
      descriptionRules: [
        (v) => !!v || 'La descripción del proyecto es requerida',
      ],
    };
  },
  methods: {
    continuarProyecto() {
      if (this.$refs.form.validate()) {
        // Realizar acciones cuando el formulario es válido
        console.log('El formulario es válido');
      } else {
        // Mostrar errores de validación
        console.log('El formulario contiene errores');
      }
    },
  },
};


 

</script>

 <!--Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.formularioUno{
   margin: 0 auto;
  max-width: 800px;
}
#imagenUno{
  filter: blur(0);
}
</style>