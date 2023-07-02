<template>
  <div class="about">
   <p class="font-weight-bold w-400 display-1 text-center my-4">
      Formulario de contacto entre los equipos
    </p>

     <v-card class="mx-auto" :width="customWidth" color="#FFAB91" outlined>
      <v-row> 
      <v-col cols="6">      
          <v-card-text>
            <p class="font-weight-medium my-5 mx-4">
              Aquí tienes el espacio para dejar un mensaje a los miembros de tu equipo sobre lo que te pareció el proyecto y si le deseas hacer cambios
            </p>
         </v-card-text>
         </v-col>
         <v-col cols="6"> 
            <v-img
              :src="require('@/assets/trabajo.png')"
              alt="gente sentada"
              :max-width="355"
              :max-height="289"
              class="my-4 v-image__image--preload"
            ></v-img>
          </v-col>
        </v-row>   
    

       


      <v-form  
   ref="form"
   v-model="valid"
   lazy-validation
   class="mx-10">
     <v-text-field
      v-model="nombreProyecto"
      :rules="nameRules"      
      label="Ingrese nombre del equipo"
      required     
    ></v-text-field>
    <v-text-field
      v-model="responsableProyecto"
      :rules="emailRules"
      label="Ingrese su telefono"
      required      
    ></v-text-field>

     <v-text-field
      v-model="responsableProyecto"
      :rules="emailRules"
      label="Ingrese su e-mail"
      required      
    ></v-text-field>

        <v-select
      v-model="select"
      :items="items"
      :rules="[v => !!v || 'Item is required']"
      label="Indique qué rol desempeña en el equipo"
      required
    ></v-select>

    <v-container fluid>
      <v-textarea
      v-model="descripcionProyecto"
       :rules="descriptionRules"        
       label="Comentarios"
      ></v-textarea>
    </v-container>

     <v-btn
      class="mr-4 my-4"
      @click="continuarProyecto"
      color="#FFE082">
      Continuar
    </v-btn>
  </v-form>
  </v-card>
 


     <p class="font-weight-bold w-400 display-1 text-center my-4">
      Lista de Proyectos
    </p>

    <v-simple-table dark class="my-20">
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
          Nombre del equipo
          </th>
          <th class="text-left">
          Telefono
          </th>
          <th class="text-left">
           e-mail
          </th>  
          <th class="text-left">
          comentarios
          </th>     
         </tr>       
        </thead>         
     


      <tbody>
          <tr v-for="proyecto in listaProyectos" :key="proyecto.nombreProyecto">
            <td>{{ proyecto.nombreProyecto }}</td>
            <td>{{ proyecto.descripcionProyecto }}</td>
            <td>{{ proyecto.responsableProyecto }}</td>
           
          </tr>
        </tbody>
     </template>
       </v-simple-table>    
  
       
    

 
  </div>
</template>  

   


   



 


<script>
export default {
  data() {
    return {
      customWidth: '1138px',
      customHeight: '572px', 
          select: null,
      items: [
        'Lider',
        'Desarrollador',
        'Diseñador',
        'Tester',
      ],
      checkbox: false,
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




