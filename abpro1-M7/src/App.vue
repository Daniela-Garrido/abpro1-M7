<script setup>
import { ref , onMounted, computed } from 'vue';
import Navbar from './components/Navbar.vue';
import CatalogoProductos from './components/CatalogoProductos.vue';

// Datos de productos (pueden venir de una API o base de datos)
const productos = ref([
  {
    id:1,
    name: 'Mouse Gamer',
    precio: 25000,
    imagen: './img/mouse.png', 
    stock: 50,
    descripcion: 'Mouse gamer con alta precision',
  },
  {
    id:2,
    name: 'Teclado Gamer',
    precio: 150000,
    imagen: './img/teclado.png', 
    stock: 0,
    descripcion: 'Teclado gamer con alta precision'
  },
  {
    id:3,
    name: 'Monitor Gamer',
    precio: 1250000,
    imagen: './img/monitor.png',
    stock: 10,
    descripcion: 'Monitor gamer con alta precision'
  },
  {
    id:4,
    name: 'Silla Gamer',
    precio: 850000,
    imagen: './img/silla.png',
    stock: 5,
    descripcion: 'Silla gamer con alta precision'
  },
  {
    id:5,
    name: 'Audifonos Gamer',
    precio: 350000,
    imagen: './img/audifonos.png',
    stock: 15,
    descripcion: 'Audifonos gamer con alta precision'
  }
]);

// === LÓGICA DEL CARRITO (Estado Reactivo) ===
const carrito = ref([]);

// Computada para calcular el total
const totalCarrito = computed(() => {
  return carrito.value.reduce((total, item) => total + (item.precio * item.cantidad), 0);
});

// Computada para contar el total de ítems
const contadorCarrito = computed(() => {
    return carrito.value.reduce((total, item) => total + item.cantidad, 0);
});


// FUNCIÓN para añadir un producto al carrito
const agregarACarrito = (producto) => {
    // 1. Verificar si el producto ya existe
    const itemIndex = carrito.value.findIndex(item => item.id === producto.id);

    if (itemIndex !== -1) {
        // 2. Si existe, aumentar la cantidad
        carrito.value[itemIndex].cantidad++;
    } else {
        // 3. Si no existe, añadirlo con cantidad 1
        const itemConCantidad = { ...producto, cantidad: 1 };
        carrito.value.push(itemConCantidad);
    }
};


// FUNCIÓN para vaciar el carrito
const vaciarCarrito = () => {
    if (confirm("¿Estás seguro que deseas vaciar el carrito?")) {
        carrito.value = [];
        alert("Carrito vaciado correctamente.");
    }
};

// FUNCIÓN para aumentar la cantidad
const aumentarCantidad = (index) => {
    // Asegúrate de que no estás agotando el stock si fuera necesario validar
    carrito.value[index].cantidad++;
};

// FUNCIÓN para disminuir la cantidad
const disminuirCantidad = (index) => {
    if (carrito.value[index].cantidad > 1) {
        carrito.value[index].cantidad--;
    } else {
        // Si la cantidad es 1 y se disminuye, se elimina el ítem
        eliminarItem(index);
    }
};

// FUNCIÓN para eliminar completamente un ítem
const eliminarItem = (index) => {
    // Usa splice para eliminar un elemento del array por su índice
    carrito.value.splice(index, 1);
};

// FUNCIÓN al presionar Comprar
const finalizarCompra = () => {
    if (carrito.value.length > 0) {
        alert("¡Compra realizada con éxito! Total a pagar: $" + totalCarrito.value.toLocaleString('es-CL'));
        vaciarCarrito(); // Vacía el carrito después de la "compra"
    } else {
        alert("Tu carrito está vacío. ¡No hay nada que comprar!");
    }
};


// Hook para el ciclo de vida (opcional, solo para seguimiento)
onMounted(() => {
    console.log("Component mounted " + productos.value.length);
});


</script>

<template>
  <div>
    <Navbar 
    :carrito="carrito" 
    :total="totalCarrito" 
    :contador-carrito="contadorCarrito" 
    @vaciar="vaciarCarrito"
    @aumentar="aumentarCantidad"
    @disminuir="disminuirCantidad"
    @eliminar="eliminarItem"
    @comprar="finalizarCompra"
/>

    <main>
      <h1 class="text-center">Productos</h1>
      <CatalogoProductos 
        :productos="productos" 
        @agregar-carrito="agregarACarrito"
      />    
    </main>
  </div>
</template>