<script setup>
import { defineProps } from 'vue';
const props = defineProps({
    producto: {
        type: Object,
        required: true
    }
});

const emit = defineEmits({
    'ver-detalle': (detalle) => {
        const ok = typeof detalle === 'object' && detalle !== null && 'id' in detalle && 'name' in detalle
        if (!ok) {
            console.warn('El evento ver-detalle requiere un objeto con id y name');
        }
        return ok
    }
})

function emitirEvento() {
    emit('ver-detalle', { id: props.producto.id, name: props.producto.name });
}

</script>
<template>
    <div class="tarjeta-producto" :class="{'producto-agotado': producto.stock === 0}" style="width: 18rem;">
        <img :src="producto.imagen" class="card-img-top" :alt="producto.name" />
        <div class="card-body">
            <h5 class="card-title">{{ producto.name }}</h5>
            <p class="card-text">{{ producto.descripcion }}</p>
            <p :class="{'text-success': producto.stock > 0, 'text-danger': producto.stock === 0}">
                <span v-if="producto.stock > 0">En stock: {{ producto.stock }}</span>
                <span v-else class="agotado">Agotado</span>
            </p>
            <button 
                @click="emitirEvento" 
                :disabled="producto.stock === 0"
                :class="{'btn-primary': producto.stock > 0, 'btn-secondary': producto.stock === 0}">
                Agregar al carrito
            </button>
        </div>
    </div>    
</template>

<style scoped>
.tarjeta-producto {
    border: 1px solid #dee2e6;
    border-radius: 0.375rem;
    transition: all 0.3s ease;
}

.tarjeta-producto:hover {
    box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15);
}

.producto-agotado {
    opacity: 0.7;
    background-color: #f8f9fa;
    border-color: #ff949f;
}

.agotado {
    font-weight: bold;
}

/* Estilos para el botón deshabilitado */
button:disabled {
    cursor: not-allowed;
}
</style>
