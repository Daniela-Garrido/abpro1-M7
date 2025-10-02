<script setup> 
import { defineProps } from 'vue';
import TarjetaProducto from './TarjetaProducto.vue';

const props = defineProps({
    productos: {
        type: Array,
        required: true
    }
});

</script>

<template> 
    <div class="catalogo-productos">
        <TarjetaProducto 
        v-for="producto in productos" 
        :key="producto.id" 
        :producto="producto"/>
    </div>
    
</template>