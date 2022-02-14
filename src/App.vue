<template>
  <div id="app" class ="abs-center">
    <img alt="Vue logo" src="./assets/logo.png">
    <p>Rellene el formulario para participar en nuestro sorteo:</p>
    <label for="nombre">Nombre:</label>
    <input id="nombre" type="text" v-model="nombre" /> <br />
    <label for="apellido1">Apellido 1:</label>
    <input id="apellido1" type="text" v-model="apellido1" /> <br />
    <label for="apellido2">Apellido 2:</label>
    <input id="apellido2" type="text" v-model="apellido2" /> <br />
    <label for="dni">DNI :</label>
    <input id="dni" type="text" v-model="dni" /> <br />
    <label for="direccion">Direccion:</label>
    <input id="direccion" type="text" v-model="direccion" /> <br />
    <label for="cp">Codigo Postal:</label>
    <input id="cp" type="number" v-model="cp" /> <br />
    <button v-on:click="addPersona()">Participar</button>
    <ul id="v-for-object">
      <li id="campos" v-for="(p, index) in personas" :key="p.id">
        {{ p.nombre }} {{ p.apellido1 }} {{ p.apellido2 }} {{ p.dni }} {{ p.direccion }}
        {{ p.cp }}
        <button class="btn-primary" id="eliminar" v-on:click="deletePersona(index)">Elimina</button>
      </li>
    </ul>
    <p v-if="error != ''">
      {{ error }}
    </p>
  </div>
</template>

<script>
export default {
  name: "App",
  data: function () {
    return {
      personas: [],
      nombre: "",
      apellido1: "",
      apellido2: "",
      dni: "",
      direccion: "",
      cp: 0,
      error: "",
    };
  },
  mounted: function () {
    this.node_env = process.env.NODE_ENV;
  },
  methods: {
    addPersona: function () {
      if (this.nombre && this.apellido1 && this.apellido2 && this.dni) {
        this.personas.push({
          nombre: this.nombre,
          apellido1: this.apellido1,
          apellido2: this.apellido2,
          dni: this.dni,
          direccion: this.direccion,
          cp: this.cp,
        });
        (this.nombre = ""),
        (this.apellido1 = ""),
        (this.apellido2 = ""),
        (this.dni = ""),
        (this.direccion = ""),
        (this.cp = 0),
        (this.error = "");
        return this;
      } else {
        this.error = "Rellena todos los campos.";
        return this;
      }
    },
    deletePersona: async function (index) {
      return this.personas.splice(index, 1);
    },
  },
};
</script>

<style>
.abs-center {
  display: flex;
  align-items: center;
  flex-direction: column;
  margin: 10px;
  min-height: 100vh;
}
</style>
