<script setup>
import { ref , onMounted } from 'vue';
import CatalogoProductos from './components/CatalogoProductos.vue';


const productos = ref([
  {
    id:1,
    name: 'Mouse Gamer',
    precio: 25000,
    imagen: 'https://media.spdigital.cl/thumbnails/products/dlzbcuza_5a4d38a9_thumbnail_512.jpg',
    stock: 50,
    descripcion: 'Mouse gamer con alta precision'
  },
  {
    id:2,
    name: 'Teclado Gamer',
    precio: 150000,
    imagen: 'https://row.hyperx.com/cdn/shop/files/hyperx_alloy_origins_60_ar_angle_5.jpg?v=1737968262&width=1946',
    stock: 0,
    descripcion: 'Teclado gamer con alta precision'
  },
  {
    id:3,
    name: 'Monitor Gamer',
    precio: 1250000,
    imagen: 'https://media.spdigital.cl/thumbnails/products/dlzbcuza_5a4d38a9_thumbnail_512.jpg',
    stock: 10,
    descripcion: 'Monitor gamer con alta precision'
  },
  {
    id:4,
    name: 'Silla Gamer',
    precio: 850000,
    imagen: 'https://media.spdigital.cl/thumbnails/products/dlzbcuza_5a4d38a9_thumbnail_512.jpg',
    stock: 5,
    descripcion: 'Silla gamer con alta precision'
  },
  {
    id:5,
    name: 'Audifonos Gamer',
    precio: 350000,
    imagen: 'https://media.spdigital.cl/thumbnails/products/dlzbcuza_5a4d38a9_thumbnail_512.jpg',
    stock: 15,
    descripcion: 'Audifonos gamer con alta precision'
  }
])

onMounted(() => {
  console.log('Component mounted', productos.value.length);
});

</script>

<template>

  <main>
   
          <h1>Productos</h1>
          <CatalogoProductos :productos="productos" />
        

  </main>

</template>

<style scoped></style>