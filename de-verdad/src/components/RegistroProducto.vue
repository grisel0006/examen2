<script setup lang="ts">
import { ref } from 'vue'
import { useProductStore } from '@/stores/productStore'

const productStore = useProductStore()

const formulario = ref({
  nombre: '',
  precio: 0,
  stock: 0
})

const enviarFormulario = () => {
  if (formulario.value.stock > 0) {
    productStore.guardarProducto({ ...formulario.value })
    formulario.value = {
      nombre: '',
      precio: 0,
      stock: 0
    }
  } else {
    alert('El stock debe ser mayor a 0')
  }
}
</script>

<template>
  <div class="container mt-4">
    <form @submit.prevent="enviarFormulario" class="row g-3">
      
      <div class="col-12 col-md-6">
        <label class="form-label">Nombre del Producto</label>
        <input v-model="formulario.nombre" type="text" class="form-control" required />
      </div>

      <div class="col-12 col-md-6">
        <label class="form-label">Precio</label>
        <input v-model.number="formulario.precio" type="number" class="form-control" required />
      </div>

      <div class="col-12 col-md-6">
        <label class="form-label">Stock</label>
        <input v-model.number="formulario.stock" type="number" class="form-control" required />
      </div>

      <div class="col-12">
        <button type="submit" class="btn btn-primary">Registrar Producto</button>
      </div>
      
    </form>
  </div>
</template>