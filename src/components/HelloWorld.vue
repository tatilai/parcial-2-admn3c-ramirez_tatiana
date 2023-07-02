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

           <v-dialog>
             <v-card>            
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="blue darken-1"
                text
                @click="close"
              >
                Cancel
              </v-btn>
              <v-btn
                color="blue darken-1"
                text
                @click="save"
              >
                Save
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>

        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="text-h5">¿Estás seguro de querer eliminar el item?</v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="closeDelete">Cancelar</v-btn>
              <v-btn color="blue darken-1" text @click="deleteItemConfirm">OK</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      
  <v-icon
    small
    class="mr-2"
    @click="editItem(item)"
  >
    mdi-pencil
  </v-icon>
  <v-icon
    small
    @click="deleteItem(item)"
  >
    mdi-delete
  </v-icon>       

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

        if (this.proyectoModificado === null) {
          this.validar = true;
          this.vacio = false;
            listaProyectos.push(proyecto);

        localStorage.setItem('proyectos', JSON.stringify(listaProyectos));

        this.listaProyectos = listaProyectos;

          const proyecto = {
            nombreProyecto: this.nombreProyecto,
            responsableProyecto: this.responsableProyecto,
            descripcionProyecto: this.descripcionProyecto,
            estado: 'En progreso'
          };

          const proyectosGuardados = localStorage.getItem('proyectos');
          let listaProyectos = [];

          if (proyectosGuardados) {
            listaProyectos = JSON.parse(proyectosGuardados);
          }

          listaProyectos.push(proyecto);

          localStorage.setItem('proyectos', JSON.stringify(listaProyectos));

          this.listaProyectos = listaProyectos;

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
   
      editItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      deleteItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialogDelete = true
      },

      deleteItemConfirm () {
        this.desserts.splice(this.editedIndex, 1)
        this.closeDelete()
      },

      close () {
        this.dialog = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      closeDelete () {
        this.dialogDelete = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
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