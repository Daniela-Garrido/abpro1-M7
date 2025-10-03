<script setup>
import { ref } from 'vue';
</script> 


<template>
  <div class="navbar bg-dark" data-bs-theme="dark">
  <div class="container-fluid">
    <a class="navbar-brand text-white font-weight-bold" href="#">
      TECNOLOLOGY STORE
    </a>
    <li class="nav-item">
                        <button class="btn btn-dark position-relative" data-bs-toggle="offcanvas"
                            data-bs-target="#offcanvasCarrito">
                            <span class="navbar-text position-relative text-white">
      Carrito de Compras <i class="bi bi-cart ms-2"></i>
    </span>
                            <span
                                class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger">
                                {{ contadorCarrito }}
                            </span>
                        </button>
                    </li>
  </div>
</div>

<div class="offcanvas offcanvas-end custom-offcanvas" tabindex="-1" id="offcanvasCarrito">
        <div class="offcanvas-header">
            <button type="button" class="btn-close" data-bs-dismiss="offcanvas"></button>
        </div>
        <div class="offcanvas-body">

            <CartDetail :carrito="carrito" :total="total" @eliminar="(i) => emit('eliminar', i)"
                @vaciar="() => emit('vaciar')" @comprar="() => emit('comprar')" @aumentar="(i) => emit('aumentar', i)"
                @disminuir="(i) => emit('disminuir', i)" />
        </div>
    </div>
</template>  