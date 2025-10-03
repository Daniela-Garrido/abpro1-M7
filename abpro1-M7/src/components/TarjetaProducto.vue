<script setup>
import { defineProps, defineEmits, onBeforeMount, onMounted, onBeforeUnmount } from 'vue';

const props = defineProps({
    producto: {
        type: Object,
        required: true
    }
});

//Definir los eventos que puede emitir el componente
const emit = defineEmits(['seleccionar-producto']);

//Función para emitir el evento al hacer clic
const seleccionar = () => {
    emit('seleccionar-producto', props.producto);
};

// Hook "created" simulado: se ejecuta al iniciar el script setup
console.log(`TarjetaProducto "${props.producto.name} (id:${props.producto.id})" creada`);

// Hook "beforeMount"
onBeforeMount(() => {
    console.log(`TarjetaProducto "${props.producto.name} (id:${props.producto.id})" antes de montarse`);
});

// Hook "mounted": cuando el componente está en el DOM
onMounted(() => {
    console.log(`TarjetaProducto "${props.producto.name} (id:${props.producto.id})" montada`);
});

// Hook "beforeUnmount": antes de que se destruya el componente
onBeforeUnmount(() => {
    console.log(`TarjetaProducto "${props.producto.name} (id:${props.producto.id})" destruida`);
});

</script>

<!-- <template> 
    <div class="tarjeta-producto">
        <img :src="producto.imagen" :alt="producto.name" />
        <h2>{{ producto.name }}</h2>
        <p>{{ producto.descripcion }}</p>
        <p>Precio: ${{ producto.precio }}</p>
        <p v-if="producto.stock > 0">En stock: {{ producto.stock }}</p>
        <p v-else class="agotado">Agotado</p>
        <button :disabled="producto.stock === 0">Agregar al carrito</button>
    </div>
    
</template> -->

<template> 
    <div class="card h-100 shadow-sm" @click="seleccionar" style="cursor: pointer;">
        <img :src="producto.imagen" class="card-img-top p-3" :alt="producto.name" :style="{height: '150px', objectFit: 'contain', filter: producto.stock === 0 ? 'grayscale(100%)' : 'none', opacity: producto.stock === 0 ? 0.5 : 1 }" />
        <div class="card-body d-flex flex-column">
            <h5 class="card-title text-truncate">{{ producto.name }}</h5>
            <p class="card-text text-muted small mb-1">{{ producto.descripcion.substring(0, 40) }}...</p>
            <p class="card-text fw-bold mt-auto mb-2">Precio: ${{ producto.precio.toLocaleString('es-CL') }}</p>
            <p class="card-text">
                <span v-if="producto.stock > 0" class="badge bg-success">Stock: {{ producto.stock }}</span>
                <span v-else class="badge bg-secondary">Stock: {{ producto.stock }}</span>
            </p>
            <button :class="['btn btn-sm', producto.stock === 0 ? 'btn-secondary' : 'btn-primary']" :disabled="producto.stock === 0">Agregar</button>
        </div>
        <slot name="ribbon"></slot>
    </div>
    
</template>
