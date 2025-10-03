<script setup> 
import { defineProps, ref } from 'vue';
import TarjetaProducto from './TarjetaProducto.vue';
import DetalleProducto from './DetalleProducto.vue';

const props = defineProps({
    productos: {
        type: Array,
        required: true
    }
});

// estado reactivo para el producto seleccionado
const productoSeleccionado = ref(null);

//Función para manejar el evento de selección
const manejarSeleccion = (producto) => {
    console.log('Producto seleccionado para detalle:' , producto.name);
    //Asigna el producto recibido al estado reactivo
    productoSeleccionado.value = producto;
};
// Función para cerrar el detalle
const cerrarDetalle = () => {
    productoSeleccionado.value = null;
    console.log('Detalle del producto cerrado. ');
};

</script>

<!-- <template> 
    <div class="catalogo-productos">
        <TarjetaProducto 
        v-for="producto in productos" 
        :key="producto.id" 
        :producto="producto"/>
    </div>
    
</template> -->

<template> 
    <div class="container my-5">
        
        <div v-if="productoSeleccionado" class="detalle-producto-container">
            <div class="d-flex justify-content-end mb-2">
                <button @click="cerrarDetalle" class="btn btn-outline-secondary btn-sm">
                    Cerrar Detalle 
                </button>
            </div>
            <DetalleProducto :producto="productoSeleccionado" />
            <hr>
            <h2 class="mt-4">Otros Productos</h2>
        </div>
        
        <div class="row row-cols-1 row-cols-md-3 row-cols-lg-5 g-4">
            <div 
                v-for="producto in productos" 
                :key="producto.id" 
                class="col"
            >
                <TarjetaProducto 
                    :producto="producto"
                    @seleccionar-producto="manejarSeleccion" 
                />
            </div>
        </div>
    </div>
</template>