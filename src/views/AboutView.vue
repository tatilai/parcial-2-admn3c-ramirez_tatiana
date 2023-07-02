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
    :lazy-src="require('@/assets/trabajo.png')"
     alt="Descripción de la imagen"
     aspect-ratio="16/9"
    :fluid="true"
    ></v-img>

    <v-card-actions>
      <v-btn
        outlined
        rounded
        text
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




