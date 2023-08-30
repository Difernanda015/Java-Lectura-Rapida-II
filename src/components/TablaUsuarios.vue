<template>
  <div class="container">
      <h1>Tabla de Usuarios</h1>
      <table>
          <thead>
              <tr>
                  <th>Id</th>
                  <th>Nombre</th>
                  <th>Apellido</th>
                  <th>Identificacion</th>
                  
              </tr>
          </thead>
          <tbody>
            
            <tr v-for="usuario in usuarios" :key="usuario.id">
                  <td>{{ usuario.id }}</td>
                  <td>{{ usuario.nombre }}</td>
                  <td>{{ usuario.apellido }}</td>
                  <td>{{ usuario.Identificacion }}</td>
              </tr>
                 
              <router-view />
          
            
          </tbody>
      </table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      usuarios: [],
    };
  },
  methods: {
    obtenerUsuarios() {
      // Método para obtener la lista de todos los estudiantes
      axios.get("http://localhost:8080/api/usuarios/listar")
      .then((response) => {
        this.usuarios = response.data;
      })
      .catch((error) => {
        console.error("Error al obtener usuarios:", error);
      });
    },
  },
  mounted() {
    // Llamar al método para obtener la lista de estudiantes al cargar el componente
    this.obtenerUsuarios();
  },
};


</script>



<style>
</style>
