<script setup lang="ts">
import { ref } from 'vue'
// Nota: 'useProductStore' es un ejemplo, asegúrate de que coincida con el nombre de tu store
import { useProductStore } from '@/stores/productStore'

// Inicializamos el store de productos
const productStore = useProductStore()

// b. Creamos el objeto reactivo vinculado a los campos del formulario
const formulario = ref({
  nombre: '',
  precio: 0,
  stock: 0
})

// d. Implementamos la función enviarFormulario() con las validaciones requeridas
const enviarFormulario = () => {
  // Valida que el stock sea mayor a 0
  if (formulario.value.stock > 0) {
    // Invoca la acción del store para guardar el producto
    productStore.guardarProducto({ ...formulario.value })
    
    // Limpia los campos del formulario después del registro
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