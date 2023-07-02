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
      v-model="nombreProyecto"
      :rules="nameRules"      
      label="Nombre del proyecto"
      required     
    ></v-text-field>
    <v-text-field
      v-model="responsableProyecto"
      :rules="emailRules"
      label="Responsable"
      required      
    ></v-text-field>

    <v-container fluid>
      <v-textarea
      v-model="descripcionProyecto"
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

     <p class="font-weight-bold w-400 display-1 text-center my-4">
      Lista de Proyectos
    </p>

    <v-simple-table dark class="my-20">
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            Nombre
          </th>
          <th class="text-left">
            Descripción del proyecto
          </th>
          <th class="text-left">
            Responsable del proyecto
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
        
    

   
     <!-- <v-dialog v-model="dialog" max-width="500px">
      <v-card>
        <v-card-title class="text-h5">Editar Proyecto</v-card-title>
        <v-card-text>
          <v-text-field v-model="editedItem.nombreProyecto" label="Nombre del proyecto"></v-text-field>
          <v-text-field v-model="editedItem.responsableProyecto" label="Responsable"></v-text-field>
          <v-textarea v-model="editedItem.descripcionProyecto" label="Descripción del proyecto"></v-textarea>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="close">Cancelar</v-btn>
          <v-btn color="blue darken-1" text @click="save">Guardar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <v-dialog v-model="dialogDelete" max-width="500px">
      <v-card>
        <v-card-title class="text-h5">Confirmar Eliminación</v-card-title>
        <v-card-text>
          ¿Estás seguro de que deseas eliminar este proyecto?
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="closeDelete">Cancelar</v-btn>
          <v-btn color="blue darken-1" text @click="deleteItemConfirm">Eliminar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>-->
  


   
    </v-form>
    
    </div>   
  </div>
</template>


<script>
export default {
  data() {
    return {
      valid: false,
      nombreProyecto: '',
      responsableProyecto: '',
      descripcionProyecto: '',
      dialog:false,
      editedItem:null,
      listaProyectos: [],
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
        if (
          this.nombreProyecto.trim().length === 0 ||
          this.descripcionProyecto.trim().length === 0 ||
          this.responsableProyecto.trim().length === 0
        ) {
          this.validar = false;
          this.mostrarError = true;
          return;
        }

         const proyecto = {
          nombreProyecto: this.nombreProyecto,
          responsableProyecto: this.responsableProyecto,
          descripcionProyecto: this.descripcionProyecto,
          estado: 'En progreso',
        };
         const proyectosGuardados = localStorage.getItem('proyectos');
        let listaProyectos = [];

        if (proyectosGuardados) {
            listaProyectos = JSON.parse(proyectosGuardados);
          }         

       listaProyectos.push(proyecto);

       localStorage.setItem('proyectos', JSON.stringify(listaProyectos));
       this.listaProyectos = listaProyectos;

        if (this.proyectoModificado === null) {
          this.validar = true;
          this.vacio = false;
            listaProyectos.push(proyecto);

        localStorage.setItem('proyectos', JSON.stringify(listaProyectos));

        

         /* const proyecto = {
            nombreProyecto: this.nombreProyecto,
            responsableProyecto: this.responsableProyecto,
            descripcionProyecto: this.descripcionProyecto,
            estado: 'En progreso'
          };

          const proyectosGuardados = localStorage.getItem('proyectos');
          let listaProyectos = [];*/

          

          

          

          

          this.nombreProyecto = '';
          this.responsableProyecto = '';
          this.descripcionProyecto = '';
          this.filtro = '';
        } else {
          this.listaProyectos[this.proyectoModificado].nombreProyecto = this.nombreProyecto;
          this.listaProyectos[this.proyectoModificado].responsableProyecto = this.responsableProyecto;
          this.listaProyectos[this.proyectoModificado].descripcionProyecto = this.descripcionProyecto;
          this.proyectoModificado = null;

          localStorage.setItem('proyectos', JSON.stringify(this.listaProyectos));

          this.nombreProyecto = '';
          this.responsableProyecto = '';
          this.descripcionProyecto = '';
        }

        console.log("continuarProyecto");
      } else {
        console.log('El formulario contiene errores');
      }
    },

     editItem(item) {
    this.editedItem = item;
    this.dialog = true;
  },

  deleteItem(item) {
    this.editedItem = item;
    this.dialogDelete = true;
  },

  deleteItemConfirm() {
    const index = this.listaProyectos.indexOf(this.editedItem);
    if (index !== -1) {
      this.listaProyectos.splice(index, 1);
      localStorage.setItem('proyectos', JSON.stringify(this.listaProyectos));
    }
    this.closeDelete();
  },

  closeDelete() {
    this.dialogDelete = false;
    this.editedItem = null;
  },

   save() {
    // Validar y guardar los cambios en el proyecto editado
    if (this.editedItem) {
      const index = this.listaProyectos.indexOf(this.editedItem);
      if (index !== -1) {
        this.listaProyectos.splice(index, 1, this.editedItem);
        localStorage.setItem('proyectos', JSON.stringify(this.listaProyectos));
      }
    }
    this.close();
    },

   close() {
    this.dialog = false;
    this.editedItem = null;
    },
   
     
  },
  mounted() {
    const proyectosGuardados = localStorage.getItem('proyectos');
    if (proyectosGuardados) {
      this.listaProyectos = JSON.parse(proyectosGuardados);
    }
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