<script setup>
import { ref , onMounted } from 'vue';
import Navbar from './components/Navbar.vue';
import CatalogoProductos from './components/CatalogoProductos.vue';


const productos = ref([
  {
    id:1,
    name: 'Mouse Gamer',
    precio: 25000,
    imagen: '/img/mouse.png',
    stock: 50,
    descripcion: 'Mouse gamer con alta precision',
  },
  {
    id:2,
    name: 'Teclado Gamer',
    precio: 150000,
    imagen: '/img/teclado.png',
    stock: 0,
    descripcion: 'Teclado gamer con alta precision'
  },
  {
    id:3,
    name: 'Monitor Gamer',
    precio: 1250000,
    imagen: '/img/monitor.png',
    stock: 10,
    descripcion: 'Monitor gamer con alta precision'
  },
  {
    id:4,
    name: 'Silla Gamer',
    precio: 850000,
    imagen: '/img/silla.png',
    stock: 5,
    descripcion: 'Silla gamer con alta precision'
  },
  {
    id:5,
    name: 'Audifonos Gamer',
    precio: 350000,
    imagen: '/img/audifonos.png',
    stock: 15,
    descripcion: 'Audifonos gamer con alta precision'
  }
])

onMounted(() => {
  console.log('Component mounted', productos.value.length);
});

</script>

<template>
  <Navbar />
  <main>
    <h1 :style="{ color: '#0d6efd', textAlign: 'center', margin: '20px 0', fontSize: '40px', fontWeight: 'bold' }">Productos</h1>
    <CatalogoProductos :productos="productos"/>
  </main>

</template>

<style scoped></style>