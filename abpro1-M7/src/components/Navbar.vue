<script setup>
import { defineProps, defineEmits } from 'vue';
import CartDetail from './CartDetail.vue'; // 🔑 Importación necesaria

// 1. Definir las PROPS para recibir los datos del carrito desde App.vue
const props = defineProps({
    carrito: {
        type: Array,
        required: true
    },
    total: {
        type: Number,
        required: true
    },
    // El contador de ítems
    contadorCarrito: {
        type: Number,
        required: true
    }
});

// 2. Definir los EMITS para comunicar las acciones del carrito a App.vue
const emit = defineEmits([
    'eliminar', 
    'vaciar', 
    'comprar', 
    'aumentar', 
    'disminuir'
]);
</script> 


<template>
  <nav class="navbar bg-dark" data-bs-theme="dark">
    <div class="container-fluid">
        <a class="navbar-brand text-white font-weight-bold" href="#">
            TECNOLOLOGY STORE
        </a>
        
        <div> 
            <button class="btn btn-dark position-relative" data-bs-toggle="offcanvas"
                data-bs-target="#offcanvasCarrito">
                <span class="navbar-text position-relative text-white">
                    Carrito de Compras <i class="bi bi-cart ms-2"></i>
                </span>
                <span class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger">
                    {{ props.contadorCarrito }}
                </span>
            </button>
        </div>
    </div>
  </nav>

<div class="offcanvas offcanvas-end custom-offcanvas" tabindex="-1" id="offcanvasCarrito">
    <div class="offcanvas-header">
        <h5 class="offcanvas-title text-dark">Carrito de Compras</h5>
        <button type="button" class="btn-close" data-bs-dismiss="offcanvas"></button>
    </div>
    <div class="offcanvas-body">
        <CartDetail
            :carrito="props.carrito"
            :total="props.total"
            @vaciar="emit('vaciar')"
            @comprar="emit('comprar')"
            @aumentar="emit('aumentar', $event)"
            @disminuir="emit('disminuir', $event)"
            @eliminar="emit('eliminar', $event)"
        />
    </div>
</div>
</template>