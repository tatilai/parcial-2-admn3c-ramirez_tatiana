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
      :error-messages="nameErrors"
      :counter="10"
      label="Nombre del proyecto"
      required
      @input="$v.name.$touch()"
      @blur="$v.name.$touch()"
    ></v-text-field>
    <v-text-field
      v-model="email"
      :error-messages="emailErrors"
      label="Responsable"
      required
      @input="$v.email.$touch()"
      @blur="$v.email.$touch()"
    ></v-text-field>

    <v-container fluid>
      <v-textarea
      v-model="email"
      :error-messages="emailErrors"
        autocomplete="descripcion"
        label="Descripcion del proyecto"
      ></v-textarea>
    </v-container>

     <v-btn
      class="mr-4"
      @click="submit"
      color="#FFE082"
    >
      Continuar
    </v-btn>
    <v-btn @click="clear">
      clear
    </v-btn>
    </v-form>
    
    </div>



   
  </div>
</template>

/*<script>

</script>

 Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.formularioUno{
   margin: 0 auto;
  max-width: 800px;
}
#imagenUno{
  filter: blur(0);
}
</style>