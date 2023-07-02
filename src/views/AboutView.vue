<template>
  <div class="about">
   <p class="font-weight-bold w-400 display-1 text-center my-4">
      Formulario de contacto entre los equipos
    </p>
      <v-card
    class="mx-auto"
    :width="customWidth"
    :height="customHeight"
    color="#FFAB91"
    outlined
    >
      <p class="font-weight-medium my-5 mx-4">
      Aqui tienes el espacio para dejar un mensaje a los miembros de tu equipo sobre lo que te parecio el proyecto y si le deseas hacer cambios
    </p>


    <v-img
    :src="require('@/assets/trabajo.png')"
    alt="gente sentada"
    :max-width="355"
    :max-height="289"   
    class="my-4 v-image__image--preload"
    ></v-img>



    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn
        outlined
        rounded
        text
        style="margin-right:30px"       
      >
        Button
      </v-btn>
    </v-card-actions>
  </v-card>
  </div>
</template>


<script>
export default {
  data() {
    return {
      customWidth: '1138px', // Establece el ancho personalizado aquí
      customHeight: '572px', // Establece el alto personalizado aquí
    };
  },
  // Resto del código del componente
};
</script>

<style scoped>
.v-image__image--preload{
  filter: blur(0);
}

</style>




