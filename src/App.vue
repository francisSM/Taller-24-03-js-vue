<template>
  <div id="app">
    <h1>CRUD de Nombres</h1>

    <form @submit.prevent="agregarNombre">
      <label for="nombre">Nombre:</label>
      <input type="text" id="nombre" v-model="nuevoNombre">
      <label for="apellido">Apellido:</label>
      <input type="text" id="apellido" v-model="nuevoApellido">
      <button type="submit">Agregar Nombre</button>
    </form>

    <hr>

    <h2>Nombres existentes: </h2>
    <ul>
      <li v-for="(nombre, index) in nombres" :key="index">
        {{ nombre.nombre }} {{ nombre.apellido }}
        <button @click="editarNombre(index)">Editar</button>
        <button @click="eliminarNombre(index)">Eliminar</button>
      </li>
    </ul>

    <div v-if="nombreEditando !== null">
      <h2>Editar Nombre</h2>
      <form @submit.prevent="guardarEdicion">
        <label for="editNombre">Nombre:</label>
        <input type="text" id="editNombre" v-model="nombres[nombreEditando].nombre">
        <label for="editApellido">Apellido:</label>
        <input type="text" id="editApellido" v-model="nombres[nombreEditando].apellido">
        <button type="submit">Guardar Cambios</button>
        <button @click="cancelarEdicion">Cancelar</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      nuevoNombre: '',
      nuevoApellido: '',
      nombres: [
        { nombre: 'Pancho', apellido: 'Pacho' },
        { nombre: 'Jose', apellido: 'Jose' },
      ],
      nombreEditando: null
    };
  },
  methods: {
    agregarNombre() {
      if (this.nuevoNombre && this.nuevoApellido) {
        this.nombres.push({
          nombre: this.nuevoNombre,
          apellido: this.nuevoApellido
        });
        this.nuevoNombre = '';
        this.nuevoApellido = '';
      }
    },
    editarNombre(index) {
      this.nombreEditando = index;
    },
    guardarEdicion() {
      this.nombreEditando = null;
    },
    cancelarEdicion() {
      this.nombreEditando = null;
    },
    eliminarNombre(index) {
      this.nombres.splice(index, 1);
    }
  }
};
</script>


<style scoped>
#app {
  font-family: Arial, sans-serif;
  max-width: 85%;
  margin: 0 auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #7cfbf2;
  min-height: 100px;
}

body{
  margin: 0; 
  padding: 0;
}

form {
  margin-bottom: 60px;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin-bottom: 15px;
}
button {
  margin-left:  10px;
}
</style>
