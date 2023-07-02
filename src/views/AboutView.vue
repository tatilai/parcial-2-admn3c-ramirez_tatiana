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
    <v-list-item three-line>
      <v-list-item-content>
        <div class="text-overline mb-4">
          OVERLINE
        </div>
        <v-list-item-title class="text-h5 mb-1">
          Headline 5
        </v-list-item-title>
        <v-list-item-subtitle>Greyhound divisely hello coldly fonwderfully</v-list-item-subtitle>
      </v-list-item-content>

      <v-list-item-avatar
        tile
        size="80"
        color="grey"
      ></v-list-item-avatar>
    </v-list-item>

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




