<template>


  <v-app>    
    <v-app-bar
      app
      color="#6d8c8e"
      dark
    >
      <div class="d-flex align-center ml-15">
       <v-img 
         alt="Logo de la app"
         class="shrink mr-2"
         contain
         :src="require('@/assets/gestion-de-proyectos.png')"
         transition="scale-transition"
         width="50" 
         height="64"
        />
        <span>ProjectPro+</span>
              
            
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
     
        <span class="mr-2">Gestión</span>
       
        <v-icon>mdi-account-cog</v-icon>
      </v-btn>
       <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
     
        <span class="mr-2">Proyectos</span>
       
        <v-icon>mdi-file-chart</v-icon>
      </v-btn>



    </v-app-bar>

    <v-main>
       <HelloWorld msg="Estamos probando vue cli"/>
      <router-view/>
    </v-main>
  </v-app>
  
  

</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  components: { HelloWorld },
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
