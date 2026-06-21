<script setup>
import {ref} from 'vue'

const expandida = ref(false)

function toggleExpandir() {
  expandida.value = !expandida.value
}

defineProps({
  producto: {
    type: Object,
    required: true
  }
})
</script>

<template>
    <section class="tarjeta-producto">
        <div class="header-slot" v-if="$slots.header">
            <slot name="header"></slot>
        </div>

        <div class="body-slot" v-if="$slots.body">
            <slot name="body" :expandida="expandida" :toggleExpandir="toggleExpandir"></slot>
        </div>

        <div class="footer-slot" v-if="$slots.footer">
            <slot name="footer">
                <span>Sin acciones disponibles</span>
            </slot>
        </div>
    </section>
</template>

<style scoped>

.tarjeta-producto {
  background: #ffffff;
  border: 2px solid #e5e7eb;
  border-radius: 12px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  transition: border-color 0.2s ease, box-shadow 0.2s ease;
  margin-bottom: 6px;
}

.tarjeta-producto:hover {
  border-color: #8260e9;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
}

.header-slot {
  padding: 16px 20px;
  border-bottom: 2px solid #e5e7eb;
}

.body-slot {
  padding: 14px 20px;
  flex: 1;
  color: #6b7280;
  font-size: 0.875rem;
  line-height: 1.6;
}

.footer-slot {
  padding: 12px 20px;
  border-top: 1px solid #e5e7eb;
  color: #9ca3af;
  font-size: 0.8rem;
}

</style>