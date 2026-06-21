<script setup>
    import TarjetaProducto from './TarjetaProducto.vue';
    import { ref } from 'vue'
    import { useTemplateRef } from 'vue';

    const props = defineProps({
    productosCargados: {
        type: Array,
        required: true
    }
    })
    const box = useTemplateRef('box')
    
    defineExpose({box})

    let expandida = ref(false)
    


</script>

<template>
    <section>
        <div ref="box" class="lista-productos">
            <p v-if="productosCargados.length === 0">
                No hay productos cargados.
            </p>

            <div v-else>
                <TarjetaProducto
                    v-for="producto in productosCargados"
                    :key="producto.id"
                    :producto="producto"
                >
                    <template #header>
                        <h3>{{producto.id}}. {{ producto.nombre }}</h3>
                    </template>

                    <template #body="{ expandida, toggleExpandir }">
                        <div v-if="expandida">
                            <p>Categoria: {{ producto.categoria }}</p>
                            <p>Precio: ${{ producto.precio }}</p>
                            <p>Stock: {{ producto.stock }}</p>
                        </div>
                        <button @click="toggleExpandir">
                            {{ expandida ? 'Ver menos' : 'Ver más' }}
                        </button>
                        
                    </template>

                    <template #footer>
                    </template>
                </TarjetaProducto>
            </div>
        </div>
    </section>
</template>

<style scoped>

.lista-productos {
  display: flex;
  flex-direction: column;
  gap: 12px;
  max-height: 600px;
  overflow-y: auto;
  padding: 25px 80px;
  background: #f3f4f6;
  border-radius: 12px;
}

.lista-productos p {
  text-align: left ;
  color: #000000;
  font-size: 0.9rem;
  padding: 10px 0;
}

.lista-productos :deep(h3) {
  font-size: 0.95rem;
  font-weight: 600;
  color: #111827;
  margin: 0;
}

.lista-productos :deep(.body-slot p) {
  font-size: 0.85rem;
  color: #34383f;
  margin: 2px 0;
}

.lista-productos :deep(.body-slot button) {
  margin-top: 8px;
  background: none;
  border: 1px solid #e5e7eb;
  border-radius: 6px;
  padding: 4px 12px;
  font-size: 0.78rem;
  color: #111827;
  cursor: pointer;
  transition: border-color 0.2s, color 0.2s;
}

.lista-productos :deep(.body-slot button:hover) {
  border-color: #a78bfa;
  color: #826cc5;
}

</style>