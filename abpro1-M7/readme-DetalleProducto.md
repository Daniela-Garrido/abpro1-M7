# Explicación de los Cambios Clave
### 1. Estado Reactivo (productoSeleccionado): 
En CatalogoProductos.vue, usamos ref(null) para guardar el producto que se desea ver en detalle. Inicialmente, es null.

### 2. Comunicación (Evento): 
En TarjetaProducto.vue, emitimos un evento personalizado (seleccionar-producto) cuando el usuario hace clic en la tarjeta.

### 3. Manejo del Evento: 
En CatalogoProductos.vue, escuchamos este evento (@seleccionar-producto="manejarSeleccion") y actualizamos productoSeleccionado.value con el producto que nos llega.

### 4. Renderizado Dinámico (v-if): 
Usamos la directiva v-if="productoSeleccionado" para renderizar condicionalmente (DetalleProducto.vue). Si el valor es un objeto de producto (no null), el componente se muestra; si es null, se oculta. Esto cumple con el requisito de componente dinámico.

### 5. Ciclo de Vida: 

Incluí los hooks onMounted y onUnmounted en DetalleProducto.vue. Observa la consola de tu navegador; verás cómo el componente se monta cuando seleccionas un producto y se desmonta cuando seleccionas otro (si estás usando la clave key en un v-for que en este caso no es necesario) o cuando cierras el detalle (cerrarDetalle).

Con estos cambios, tu proyecto ahora tiene un catálogo interactivo que muestra dinámicamente el detalle de un producto al hacer clic, y has comenzado a implementar la medición del ciclo de vida.