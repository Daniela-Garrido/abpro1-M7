<script setup>
import { defineProps, defineEmits } from 'vue';

// 1. Recibe los datos y define los eventos a emitir hacia arriba (hacia Navbar.vue)
const props = defineProps({
    carrito: {
        type: Array,
        required: true
    },
    total: {
        type: Number,
        required: true
    }
});

// 2. Define todos los eventos de interacción del carrito
const emit = defineEmits([
    'eliminar', // Eliminar un producto por índice
    'vaciar',   // Vaciar todo el carrito
    'comprar',  // Finalizar la compra
    'aumentar', // Aumentar cantidad por índice
    'disminuir' // Disminuir cantidad por índice
]);
</script>

<template>
    <div>
        <h4 class="mb-3 text-dark">Resumen de tu Carrito</h4>
        
        <div v-if="props.carrito.length > 0">
            <ul class="list-group mb-3">
                <li v-for="(item, index) in props.carrito" :key="item.id" class="list-group-item d-flex justify-content-between align-items-center lh-sm">
                    <div class="flex-grow-1 me-2">
                        <h6 class="my-0 text-dark">{{ item.name }} (x{{ item.cantidad }})</h6>
                        <small class="text-muted">{{ item.descripcion.substring(0, 30) }}...</small>
                    </div>
                    
                    <div class="d-flex align-items-center me-3">
                        <button 
                            @click="emit('disminuir', index)" 
                            class="btn btn-sm btn-outline-warning p-0 px-2 me-1"
                            :disabled="item.cantidad <= 1"
                        >
                            -
                        </button>
                        <span class="fw-bold">{{ item.cantidad }}</span>
                        <button 
                            @click="emit('aumentar', index)" 
                            class="btn btn-sm btn-outline-success p-0 px-2 ms-1"
                        >
                            +
                        </button>
                    </div>
                    
                    <span class="text-dark fw-bold me-3">
                        ${{ (item.precio * item.cantidad).toLocaleString('es-CL') }}
                    </span>
                    
                    <button @click="emit('eliminar', index)" class="btn btn-sm btn-danger p-0 px-2" title="Eliminar ítem">
                        <i class="bi bi-x"></i>
                    </button>
                </li>
            </ul>
            
            <h5 class="d-flex justify-content-between text-dark border-top pt-3">
                <span>Total</span>
                <strong class="text-success">${{ props.total.toLocaleString('es-CL') }}</strong>
            </h5>

            <div class="d-grid gap-2 mt-4">
                <button @click="emit('comprar')" class="btn btn-primary">Finalizar Compra</button>
                <button @click="emit('vaciar')" class="btn btn-outline-danger">Vaciar Carrito</button>
            </div>
            
        </div>
        
        <div v-else class="alert alert-info mt-4">
            Tu carrito está vacío. ¡Empieza a comprar!
        </div>
    </div>
</template>

<style scoped>
</style>