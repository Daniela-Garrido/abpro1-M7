<script setup>
import { defineProps } from 'vue';
const props = defineProps({
    producto: {
        type: Object,
        required: true
    }
});

</script>

<template> 
    <div class="tarjeta-producto">
        <img :src="producto.imagen" :alt="producto.name" />
        <h2>{{ producto.name }}</h2>
        <p>{{ producto.descripcion }}</p>
        <p>Precio: ${{ producto.precio }}</p>
        <p v-if="producto.stock > 0">En stock: {{ producto.stock }}</p>
        <p v-else class="agotado">Agotado</p>
        <button :disabled="producto.stock === 0">Agregar al carrito</button>
    </div>
    
</template>
