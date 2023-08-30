<template>
  <div class="container">
    <h1>Formulario de Usuarios</h1>
    <form id="student-form" @submit.prevent="guardar">
      <div class="form-group">
        <label for="id">Id</label>
        <input type="text" id="Id" name="id" required v-model="id" />
      </div>
      <div class="form-group">
        <label for="nombre">Nombre</label>
        <input type="text" id="nombre" name="nombre" required v-model="nombre" />
      </div>
      <div class="form-group">
        <label for="apellido">Apellido</label>
        <input type="text" id="apellido" name="apellido" required v-model="apellido" />
      </div>
      <div class="form-group">
        <label for="identificacion">Identificacion</label>
        <input type="number" id="identificacion" name="identificacion" required v-model="identificacion" />
      </div>

        <button type="submit" id="guardar" name="guardar">Guardar</button><br/>
        <button type="button" id="eliminar" name="eliminar" @click="eliminar">Eliminar</button><br/>
        <button type="button" id="actualizar" name="actualizar" @click="actualizar">Actualizar</button><br/>
        <button type="button" id="consultar" name="consultar" @click="consultar">Consultar</button><br/>

    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  
  data() {

    return {
      id: "",
      nombre: "",
      apellido: "",
      identificacion: null,
    };

  },

  methods: {
    guardar() {
      axios
      .post("http://localhost:8080/api/Usuarios", {
        id: this.id,
        nombre: this.nombre,
        apellido: this.apellido,
        identificacion: this.identificacion,

      })
      .then((Response)=>{
        console.log("Usuario registrado con exito", Response.data);
        alert("Exito");
        this.id="";
        this.nombre="";
        this.apellido="";
        this.identificacion="";

      })

      .catch((error) => {
        console.error("Error al registrar usuario:", error);
        });
      },

      consultar() {
      
      axios
      .get('http://localhost:8080/api/usuarios/'+this.id)
      .then((response) => {
          // Actualizar los campos del formulario con los datos del estudiante consultado
          this.nombre = response.data.nombre;
          this.apellido = response.data.apellido;
          this.identificacion = response.data.identificacion;
        })
        .catch((error) => {
          console.error("Error al consultar usuario:", error);
        
        });
    },
    actualizar() {
      
      axios
        .put("http://localhost:8080/api/usuarios/actualizar/"+this.id, {
          id:this.id,
          nombre: this.nombre,
          apellido: this.apellido,
          identificacion: this.identificacion,
        })
        .then((response) => {
          console.log("Usuario actualizado con éxito:", response.data);
        })
        .catch((error) => {
          console.error("Error al actualizar Usuario:", error);
        });
    },

    eliminar() {
     
     axios
       .delete("http://localhost:8080/api/usuarios/"+this.id)
       .then(() => {
         console.log("Usuario eliminado con éxito");
         // Limpiar los campos del formulario después de eliminar
         this.id = "";
         this.nombre = "";
         this.apellido = "";
         this.identificacion = null;
       })
       .catch((error) => {
         console.error("Error al eliminar usuario:", error);
       });
   },
 },
};


  


</script>


<style>
</style>
