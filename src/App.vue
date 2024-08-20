<script setup>
  import axios from "axios"
import { ref } from "vue";

const producto = ref({})

  const datos = ref([])

  async function obtenerProductos(){
    //alert("Probando...")
    const {data} = await axios.get('http://127.0.0.1:3000/producto');

    datos.value = data
  }

  obtenerProductos()

  async function guardarProducto(){
    await axios.post("http://127.0.0.1:3000/producto", producto.value) 

    obtenerProductos();
  }

</script>

<template>
  <h1>Productos</h1>
  <h2>Nuevo producto</h2>

  <label for="">Ingrese nombre</label>
  <input type="text" v-model="producto.nombre">
  <br>
  <label for="">Ingrese Precio</label>
  <input type="text" v-model="producto.precio">
  <br>
  <label for="">Ingrese Cantidad</label>
  <input type="text" v-model="producto.cantidad">
  <br>
  <label for="">Ingrese Descripción</label>
  <input type="text" v-model="producto.descripcion">
  <br>
  <label for="">Ingrese Imagen</label>
  <input type="text" v-model="producto.imagen">
  <br>
  <button @click="guardarProducto()">Guardar Producto</button>
  
  {{producto}}

  <h2>Lista de productos</h2>

  <table class="table table-striped">
    <thead>
      <tr>
        <th>Nombre</th>
        <th>Precio</th>
        <th>Cantidad</th>
        <th>Descripción</th>
        <th>Imagen</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="d in datos" :key="d._id">
        <td>{{d.nombre}}</td>
        <td>{{d.precio}}</td>
        <td>{{d.cantidad}}</td>
        <td>{{d.imagen}}</td>
        <td></td>
      </tr>
    </tbody>
  </table>

</template>

<style scoped>
  h1{
    color: #ff0000;
  }
  h2{
    color: #0000ff;
  }
</style>
