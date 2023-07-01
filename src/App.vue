<template>

 <div id="app"> 
  <v-app> 

   
     <v-navigation-drawer
     v-model="drawer"
     :transition="drawerTransition">   
   
      <v-list>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :style="{ marginTop: item.marginTop }" 
          link
        >

       
          <v-list-item-icon>            
            <v-icon>
              {{ item.icon }}
              </v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>
                <router-link :to="item.link">{{ item.title }}
                  </router-link> 
              </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>

      
    </v-navigation-drawer>       

          
    
 

    <v-app-bar
      app
      color="#26A69A"
      dark
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

      <nav>
          <router-link to= "/">Gestion</router-link>|
          <router-link to= "/about">Proyectos</router-link>
          
     </nav>
     <!-- <div class="d-flex align-center ml-15">
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
      </v-btn>-->



    </v-app-bar>

    <v-main>       
      <router-view/>
    </v-main>
  </v-app>
  </div>
  

</template>

<script>


export default {
  
  name: 'App',

  data: () => ({
      drawer: false,  
      drawerTransition: 'slide-x-transition',    
      items: [
          { title: 'Gestion', icon: 'mdi-account-cog',link:'/',marginTop:'50px' },
          { title: 'Proyectos', icon: 'mdi-file-chart',link:'/about' },
         
        ],
       right:null,
    }),

    
};
</script>
