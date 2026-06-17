<script setup>
  import ListaProductos from '../ListaProductos.vue';
  import { productos } from '@/data/productos.js';
  import { ref, onMounted } from 'vue'

  const productosCargados = ref([])
  const cargando = ref(false)
  let timer = null

  async function cargarProductos() {
  cargando.value = true
  await new Promise(resolve => setTimeout(resolve, 800))
  productosCargados.value = productos.filter(producto => producto.categoria === 'Electrónica')
  cargando.value = false
}


onMounted(() => {
  cargarProductos()
  timer = setInterval(cargarProductos, 10000)
})

</script>


<template>
  <p v-if="cargando">Cargando...</p>
  <ListaProductos v-else ref="listaRef" :productosCargados="productosCargados" />
</template>

<style scoped></style>