<script setup>
import { defineProps, onMounted, onUnmounted } from 'vue';

const props = defineProps({
    producto: {
        type: Object,
        required: true
    }
});

//Hook del ciclo de vida para medir el tiempo de vida
onMounted(() => {
    console.log(`DetalleProducto: ${props.producto.name} se ha montado. `);
});
onUnmounted(() => {
    console.log(`DetalleProducto: ${props.producto.name}) se va a desmontar. `);
});
</script>

<template>
    <div class="card my-4 border-dark">
        <div class="card-header bg-dark text-white">
            <h5 class="mb-0">Detalle del producto</h5>
        </div>
        <div class="card.body row align-items-center p-4">
            <div class="col-md-4 text-center">
                <img :src="producto.imagen" class="img-fluid rounded" style="max-height: 200px;" alt="producto.name" />
            </div>
            <div class="col-md-8">
                <h3 class="card-title text-primary">{{ producto.name }}</h3>
                <p class="card-text">
                    <strong class="text-secondary">Descripción:</strong> {{ producto.descripcion }}
                </p>
                <p class="card-text fs-4 fw-bold">
                    Precio: <span class="text-success">{{ producto.precio.toLocaleString('es-CL') }}</span>
                </p>
                <p class="card-text">
                    <span v-if="producto.stock > 0" class="badge bg-info text-dark">
                        En Stock: {{ producto.stock }} unidades
                    </span>
                    <span v-else class="badge bg-danger">Agotado</span>
                </p>
            </div>
        </div>
    </div>
</template>