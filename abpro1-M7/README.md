
## Módulo 7 - Desarrollo de aplicaciones Front-End con Framework Vue

### Actividad M7-ABPRO1 - Componentes y su ciclo de vida en Vue

### Integrantes:
María Teresa De La Fuente
Daniela Garrido
Gonzalo Román

### Ruta: https://github.com/Daniela-Garrido/abpro1-M7

# Descripción del Proyecto
Este proyecto consiste en un catálogo interactivo de productos tecnológicos desarrollado con Vue.js 3. La aplicación permite visualizar productos, agregarlos al carrito de compras, gestionar cantidades y finalizar compras de manera intuitiva.

## Características Principales
* Catálogo de productos con información detallada
* Carrito de compras interactivo
* Gestión de stock en tiempo real
* Componentes reutilizables y modulares
* Diseño responsive con Bootstrap
* Comunicación entre componentes mediante props y eventos


## Descripción de Componentes
### App.vue - Componente Principal
Gestiona el estado global de la aplicación
Contiene la lógica del carrito de compras
Coordina la comunicación entre componentes

### Navbar.vue - Barra de Navegación
Muestra el contador de items en el carrito
Contiene el botón para abrir el carrito
Implementa un offcanvas de Bootstrap para el carrito

### CartDetail.vue - Detalle del Carrito
Muestra resumen de productos en el carrito
Permite modificar cantidades (+/-)
Opciones para vaciar carrito y finalizar compra

### CatalogoProductos.vue - Catálogo Principal
Renderiza la grilla de productos
Gestiona la visualización del detalle de productos
Implementa slots para ribbons personalizados

### TarjetaProducto.vue - Tarjeta de Producto Individual
Componente reutilizable para mostrar cada producto
Emite eventos para agregar al carrito y ver detalle
Implementa hooks del ciclo de vida

### Slots para contenido personalizado (ribbons)

DetalleProducto.vue - Vista Detallada del Producto
Muestra información ampliada del producto

### Hook del ciclo de vida para seguimiento

## Funcionalidades Implementadas


### Gestión de Productos
Visualización de productos con imagen, nombre, precio y stock

Indicadores visuales de stock (disponible/agotado)

Ribbons dinámicos para productos agotados o con stock bajo

Vista detallada al hacer clic en "Detalle"

### Carrito de Compras

* Agregar productos al carrito
* Modificar cantidades (incrementar/decrementar)
* Eliminar productos individuales
* Vaciar carrito completo
* Cálculo automático del total
* Finalización de compra con confirmación

### Comunicación entre Componentes
* Props: Paso de datos de padre a hijo
* Emits: Comunicación de hijo a padre
* Slots: Contenido personalizable en componentes

### 🎨 Estilos y Diseño
* Framework CSS: Bootstrap
* Fuentes: Space Grotesk para títulos, Open Sans para texto

### Design System:

* Colores consistentes para estados (success, warning, danger)
* Cards con sombras y hover effects
* Badges para indicadores de stock
* Ribbons personalizados para productos especiales

## Hooks del Ciclo de Vida
* Implementados en TarjetaProducto.vue:
>onBeforeMount() - Antes de montar el componente
onMounted() - Cuando el componente está en el DOM
onBeforeUnmount() - Antes de destruir el componente

Implementados en DetalleProducto.vue:
onMounted() - Seguimiento de montaje

onUnmounted() - Seguimiento de desmontaje

## 🛒 Lógica de Negocio
* Gestión de Stock
* Validación de disponibilidad antes de agregar al carrito
* Indicadores visuales para stock bajo (≤5 unidades)
* Productos agotados se muestran en escala de grises

### Carrito de Compras
* Persistencia del estado durante la sesión
* Validación de cantidades mínimas
* Confirmaciones para acciones destructivas

## 🚀 Scripts y Configuración
El proyecto utiliza:
* Vue 3 con Composition API
* Vite como tooling de build
* Bootstrap para estilos


## 🔄 Flujo de Datos
App.vue → Props → Componentes hijos
Componentes hijos → Emits → App.vue
Estado reactivo con ref() y computed()
Validaciones en tiempo real para stock y cantidades


## Estructura 
Jerarquía de Componentes

```
abpro1-M7/
├── public/
│   ├── img/
│   │   ├── mouse.png
│   │   ├── teclado.png
│   │   ├── monitor.png
│   │   ├── silla.png
│   │   └── audifonos.png
│   └── vite.svg
├── src/
│   ├── assets/
│   ├── components/
│   │   ├── CartDetail.vue
│   │   ├── CatalogoProductos.vue
│   │   ├── DetalleProducto.vue
│   │   ├── Navbar.vue
│   │   └── TarjetaProducto.vue
│   ├── App.vue
│   ├── main.js
│   └── style.css
├── index.html
├── package.json
├── vite.config.js
└── README.md
```
