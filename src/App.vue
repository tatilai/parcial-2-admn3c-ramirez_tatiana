<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
       <v-img 
         alt="Logo de la app"
         :src="require('@/assets/gestion-de-proyectos.png')"
         width="55" 
        />
              
            
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
     
        <span class="mr-2">Gestión</span>
       
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
       <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
     
        <span class="mr-2">Proyectos</span>
       
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>



    </v-app-bar>

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
