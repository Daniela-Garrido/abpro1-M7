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
    console.log('Producto seleccionado para detalle:', producto.name);
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
        :producto="producto"
        @ver-detalle="(detalle) => alert(`id: ${producto.id}, name: ${producto.name}`)"/>
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
            <div v-for="producto in productos" :key="producto.id" class="col">
                <TarjetaProducto :producto="producto" @seleccionar-producto="manejarSeleccion">
                     <!-- Ribbon rojo: AGOTADO -->
                    <template v-if="producto.stock === 0" #ribbon>
                        <div class="ribbon ribbon-bottom-right">
                            <span class="ribbon-red">AGOTADO</span></div>
                    </template>

                    <!-- Ribbon amarillo: ÚLTIMAS UNIDADES -->
                    <template v-else-if="producto.stock <=5" #ribbon>
                        <div class="ribbon ribbon-bottom-right">
                            <span class="ribbon-yellow">ÚLTIMOS</span></div>
                    </template>
                </TarjetaProducto>
            </div>
        </div>
    </div>
</template>

<style scoped>
.ribbon {
    width: 6rem;
    height: 6rem;
    overflow: hidden;
    position: absolute;
    bottom: 0px;
    right: 0px;
}

.ribbon span {
    position: absolute;
    display: block;
    width: 20rem;
    padding: 0.3rem;
    padding-right: 2rem;
    text-align: center;
    font-weight: bold;
    transform: rotate(-45deg);
    top: 2rem;
    left: -5.5rem;
}

.ribbon-red {
    background: rgba(219, 10, 10);
    color: white;
}

.ribbon-yellow {
    background: rgb(248, 212, 8);
    color: black;
}




</style>