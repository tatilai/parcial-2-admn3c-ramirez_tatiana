<template>
  <div class="about">
   <p class="font-weight-bold w-400 display-1 text-center my-4">
      Formulario de contacto entre los equipos
    </p>

     <v-card class="mx-auto" :width="customWidth" :height="customHeight" color="#C8E6C9" outlined>
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
    style="height: 70px"
   class="mx-10">
     <v-text-field
      v-model="datosFormulario.nombre"
      :rules="nameRules"      
      label="Ingrese nombre del equipo"
      required     
    ></v-text-field>
    <v-text-field
      v-model="datosFormulario.telefono"
      :rules="phoneRules"
      label="Ingrese su telefono"
      required      
    ></v-text-field>

     <v-text-field
      v-model="datosFormulario.email"
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
      v-model="datosFormulario.descripcion"
       :rules="descriptionRules"        
       label="Comentarios"
      ></v-textarea>
    </v-container>

     <v-btn
      class="mr-4 mb-6"
      @click="guardar"
      color="#FFE082">
    Enviar
    </v-btn>
  </v-form>
  </v-card>
 


     <!-- <p class="font-weight-bold w-400 display-1 text-center my-4">
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
       </v-simple-table> -->   


   <template v-if="formularioEnviado">
     <v-card
    class="mx-auto mt-5 mb-5"
    max-width="400"

  >
    <v-img
      class="white--text align-end"
      height="200px"
     :src="require('@/assets/lista-de-verificacion_2.png')"
    
    >
      <v-card-title style="color:black">Info del formulario enviado</v-card-title>
    </v-img>

    <v-card-subtitle class="pb-0">
      Number 10
    </v-card-subtitle>

    <v-card-text class="text--primary">
  
    <v-list-item four-line>
       <v-list-item-content>
          <v-list-item-subtitle>Nombre:</v-list-item-subtitle>
          <v-list-item-subtitle>{{ datosFormulario.nombre }}</v-list-item-subtitle>
          <v-list-item-subtitle>Email:</v-list-item-subtitle>
          <v-list-item-subtitle>{{ datosFormulario.email }}</v-list-item-subtitle>
          <v-list-item-subtitle>Teléfono:</v-list-item-subtitle>
          <v-list-item-subtitle>{{ datosFormulario.telefono }}</v-list-item-subtitle>
          <v-list-item-subtitle>Comentario:</v-list-item-subtitle>
          <v-list-item-subtitle>{{ datosFormulario.comentario }}</v-list-item-subtitle>
        </v-list-item-content>
    </v-list-item>

    </v-card-text>

   
  </v-card>
   </template>    
    

 
  </div>
</template>  

   


   



 


<script>
export default {

   data() {
    return {
      customWidth: '1138px',
      customHeight: '870px', 
          select: null,
         formularioEnviado: false,
           datosFormulario: {
            nombre:"",
            email:"",
            telefono:"",
            rolSeleccionado:"",                     
            confirmacion:null        
                     
           }, 
           objetoLocal: {},
      items: [
        'Lider',
        'Desarrollador',
        'Diseñador',
        'Tester',
      ],
      checkbox: false,

      nameRules: [v => !!v || "Nombre del equipo es obligatorio"],
      phoneRules: [
        v => !!v || "Teléfono es obligatorio",
        v => /^\d{10}$/.test(v) || "Debe ingresar un formato valido por ejemplo:1565986574"
      ],
      emailRules: [
        v => !!v || "Email es obligatorio",
        v => /^\w+([.-_+]?\w+)*@\w+([.-]?\w+)*(\.\w{2,10})+$/.test(v) ||
          "Formato de email inválido"
      ],
     
      descriptionRules: [
        v => (v && v.length >= 15) || "El comentario debe tener al menos 15 caracteres"
      ],
      enviado: false,
      errores: [],
    };    
   },
    
     methods: {
    guardar() {

      this.enviado=true;  //queremos evaluar que los mensajes se muestren solo cuando se ejecute la funcion
      this.errores=[]  //vaciamos el array de errores

      if (this.$refs.form.validate()) {  
       if (
        this.nombreProyecto.trim().length === 0 ||
        this.responsableProyecto.trim().length === 0 ||
        this.emailProyecto.trim().length === 0
      ) {
        // Mostrar mensaje de error
        this.valid = false;
        this.mostrarError = true;
        return;
      }}

      if(!this.datosFormulario.nombre){

       console.log(!this.datosFormulario.nombre)
       this.errores.push('El nombre del equipo es obligatorio');

      }
      if(this.contacto.nombre && this.contacto.nombre.length < 5) {
        this.errores.push('NOMBRE: Debe tener más de 5 caracteres.');
         
      }
      if(!this.datosFormulario.comentario){
        this.errores.push('COMENTARIO:debe escribir su comentario');
      }

      let emailValido= /^\w+([.-_+]?\w+)*@\w+([.-]?\w+)*(\.\w{2,10})+$/;

      if( !emailValido.test(this.contacto.email) ){
        
        this.errores.push('EMAIL: no se corresponde con un valor válido.')

        }

      let telefonoValido= /^\d{10}$/;
      if(!telefonoValido.test(this.contacto.telefono)){
        this.errores.push('Debe ingresar un formato valido por ejemplo:1565986574')
      }  


      if(this.contacto.comentario&& this.contacto.comentario.length<15){
        this.errores.push('El comentario tiene que tener mas de 15 caracteres');
      }

      if (!this.datosFormulario.confirmacion) {

        this.errores.push('Debes confirmar que los datos son correctos')
          
      }

       this.objetoLocal = {
         comentario: this.datosFormulario.comentario,
         nombre: this.datosFormulario.nombre,
         email: this.datosFormulario.email,
         telefono: this.datosFormulario.telefono,
         rol: this.datosFormulario.rolSeleccionado
       };
       this.datosFormulario = {
      nombre: this.contacto.nombre,
      email: this.contacto.email,
      telefono: this.contacto.telefono,
      descripcion: this.contacto.descripcion
      };

      this.formularioEnviado = true;


      console.log(this.errores)

      if(this.errores.length==0){
        this.enviado=true;
        objetoLocal={
          comentario:this.contacto.comentario,
          nombre:this.contacto.nombre,
          email:this.contacto.email,
          telefono:this.contacto.telefono,
          rol: this.contacto.rolSeleccionado
        }
        if(!localStorage.dato){
          this.arr=[]
        }else{
          this.enviado=false;
          this.arr=JSON.parse(localStorage.getItem("datoComentario"))

        

        }

            this.arr.push(objetoLocal)
            localStorage.setItem("datoComentario",JSON.stringify(this.arr))

            
            
      }

    }

   
    
  }
};

</script>

<style scoped>
.v-image__image--preload{
  filter: blur(0);
}

</style>




