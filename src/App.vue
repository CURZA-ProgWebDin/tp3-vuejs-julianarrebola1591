<script setup>
  import PanelPestanas from './PanelPestanas.vue';
  import { productos } from './data/productos.js';
  import { ref, useTemplateRef, onMounted, onBeforeUnmount, onUpdated } from 'vue'

  const productosCargados = ref([])
  const cargando = ref(false)
  let timer = null
  const listaRef = useTemplateRef('listaRef')

  async function cargarProductos() {
  cargando.value = true
  await new Promise(resolve => setTimeout(resolve, 800))
  productosCargados.value = productos
  cargando.value = false
}

  function scrollAlFinal() {
  listaRef.value.box.scrollTop = listaRef.value.box.scrollHeight
}

onMounted(() => {
  cargarProductos()
  timer = setInterval(cargarProductos, 30000)
})

onBeforeUnmount(() => {
  clearInterval(timer)
  console.log('ListaProductos desmontado — polling detenido')
})

onUpdated(()=> {
  if (listaRef.value){
    scrollAlFinal()
  }

})
</script>


<template>
  <PanelPestanas></PanelPestanas>
</template>

<style scoped></style>
  