
<template>
  <div>
    <p class="font-weight-bold w-400 display-1 text-center my-4">
      Formulario de contacto entre los equipos
    </p>

    <v-card class="mx-auto" :width="customWidth" :height="customHeight" color="#C8E6C9" outlined>
      <v-card-media>
            <v-img
              :src="require('@/assets/trabajo.png')"
              alt="gente sentada"
              :max-width="355"
              :max-height="289"
              class="my-4 v-image__image--preload"
            ></v-img>
      </v-card-media>

      <v-card-text>
        <v-form @submit.prevent="guardar" ref="form">
          <v-text-field
            v-model="equipo"
            label="Nombre del equipo"
            :rules="equipoRules"
            required
          ></v-text-field>

          <v-text-field
            v-model="telefono"
            label="Teléfono"
            :rules="telefonoRules"
            required
          ></v-text-field>

          <v-text-field
            v-model="email"
            label="Email"
            :rules="emailRules"
            required
          ></v-text-field>

          <v-select
            v-model="rol"
            :items="roles"
            label="Rol en el equipo"
            :rules="rolRules"
            required
          ></v-select>

          <v-textarea
            v-model="comentarios"
            label="Comentarios"
          ></v-textarea>

          <v-btn type="submit" color="primary">Enviar</v-btn>
        </v-form>
      </v-card-text>
    </v-card>

    <h2>Información del formulario enviado</h2>

    <v-card>
      <v-card-text>
        <v-simple-table>
          <template v-slot:default>
            <thead>
              <tr>
                <th>Nombre</th>
                <th>Teléfono</th>
                <th>Email</th>
                <th>Rol</th>
                <th>Comentarios</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(datos, index) in listaDatos" :key="index">
                <td>{{ datos.equipo }}</td>
                <td>{{ datos.telefono }}</td>
                <td>{{ datos.email }}</td>
                <td>{{ datos.rol }}</td>
                <td>{{ datos.comentarios }}</td>
              </tr>
              <tr v-if="listaDatos.length === 0">
                <td :colspan="5" class="text-center">No hay datos disponibles</td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      equipo: '',
      telefono: '',
      email: '',
      rol: '',
      comentarios: '',
      listaDatos: [],
      roles: ['Lider', 'Desarrollador', 'Diseñador', 'Tester'],
      equipoRules: [
        v => !!v || 'El nombre del equipo es obligatorio',
      ],
      telefonoRules: [
        v => !!v || 'El teléfono es obligatorio',
        v => /^\d{10}$/.test(v) || 'El teléfono debe tener 10 dígitos',
      ],
      emailRules: [
        v => !!v || 'El email es obligatorio',
        v => /^\w+([.-_+]?\w+)*@\w+([.-]?\w+)*(\.\w{2,10})+$/.test(v) || 'Formato de email inválido',
      ],
      rolRules: [
        v => !!v || 'Debe seleccionar un rol',
      ],
    };
  },

   methods: {
    guardar() {
      if (!this.$refs.form.validate()) {
        return;
      }

      const datosFormulario = {
        equipo: this.equipo,
        telefono: this.telefono,
        email: this.email,
        rol: this.rol,
        comentarios: this.comentarios,
      };

      this.listaDatos.push(datosFormulario);

      this.equipo = '';
      this.telefono = '';
      this.email = '';
      this.rol = '';
      this.comentarios = '';

      this.$refs.form.resetValidation();
    },
  },
};
  
</script>


<style scoped>
.v-image__image--preload{
  filter: blur(0);
}

.formularioDos{
   margin: 0 auto;
 
}

</style>




