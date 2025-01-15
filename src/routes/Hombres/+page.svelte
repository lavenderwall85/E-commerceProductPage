<script>
  import { writable } from 'svelte/store';

  // Crear una store para los productos
  const carrito = writable([
    { id: 1, nombre: 'Running Sneakers', precio: 75.00, imagen: '/images/zapatosHombres/modelo1.jpg', descripcion: 'Comfortable running shoes', cantidad: 0 },
    { id: 2, nombre: 'Casual Sneakers', precio: 60.00, imagen: '/images/zapatosHombres/modelo2.jpg', descripcion: 'Stylish casual shoes', cantidad: 0 },
    { id: 3, nombre: 'High-Top Sneakers', precio: 85.00, imagen: '/images/zapatosHombres/modelo3.jpg', descripcion: 'Trendy high-top design', cantidad: 0 },
    { id: 4, nombre: 'High-Top Sneakers', precio: 85.00, imagen: '/images/zapatosHombres/modelo4.jpg', descripcion: 'Trendy high-top design', cantidad: 0 },
    { id: 5, nombre: 'High-Top Sneakers', precio: 85.00, imagen: '/images/zapatosHombres/modelo5.jpg', descripcion: 'Trendy high-top design', cantidad: 0 },
    { id: 5, nombre: 'High-Top Sneakers', precio: 85.00, imagen: '/images/zapatosHombres/modelo6.jpg', descripcion: 'Trendy high-top design', cantidad: 0 },
    { id: 5, nombre: 'High-Top Sneakers', precio: 85.00, imagen: '/images/zapatosHombres/modelo7.jpg', descripcion: 'Trendy high-top design', cantidad: 0 }
  ]);

  let menuAbierto = false;
  let cuentaAbierta = false;
  let imagenSeleccionada = null;

  function toggleMenu() {
    menuAbierto = !menuAbierto;
  }

  function toggleCuenta() {
    cuentaAbierta = !cuentaAbierta;
  }

  function agregarAlCarrito(producto) {
    carrito.update(items => {
      const index = items.findIndex(item => item.id === producto.id);
      if (index !== -1) {
        items[index].cantidad = items[index].cantidad === 0 ? 1 : items[index].cantidad + 1;
      }
      return items;
    });
  }

  function seleccionarImagen(imagen) {
    imagenSeleccionada = imagen;
  }

  function cambiarCantidad(producto, cantidad) {
    if (cantidad >= 0) {
      carrito.update(items => {
        const index = items.findIndex(item => item.id === producto.id);
        if (index !== -1) {
          items[index].cantidad = cantidad;
        }
        return items;
      });
    }
  }

  function eliminarProducto(producto) {
    carrito.update(items => {
      return items.map(item => {
        if (item.id === producto.id) {
          item.cantidad = 0; // Solo pone la cantidad en 0, no elimina el producto
        }
        return item;
      });
    });
  }
</script>

<nav class="menu">
  <div class="logo">sneakers</div>
  <ul class="menu-links">
    <li><a href="/Home">Colecciones</a></li>
    <li><a href="/Hombres">Hombres</a></li>
    <li><a href="/Mujeres">Mujeres</a></li>
    <li><a href="/AcercaDe">Acerca de</a></li>
    <li><a href="/Contacto">Contacto</a></li>
  </ul>
  <div class="menu-icons">
    <span class="carrito" on:click={toggleMenu}>🛒</span>
    <span class="avatar" on:click={toggleCuenta}>👤</span>
  </div>
</nav>

{#if menuAbierto}
  <div class="cart">
    <h1>Carrito</h1>
    {#each $carrito as producto}
      {#if producto.cantidad > 0}
        <div class="producto-en-carrito">
          <img src={producto.imagen} alt={producto.nombre} class="producto-img" />
          <div class="producto-info">
            <div class="producto-texto">
              <p class="producto-nombre">{producto.nombre}</p>
              <p class="producto-precio">${(producto.precio * producto.cantidad).toFixed(2)}</p>
            </div>
            <button class="eliminar" on:click={() => eliminarProducto(producto)}>Eliminar</button>
          </div>
        </div>
      {/if}
    {/each}
  </div>
{/if}

{#if cuentaAbierta}
  <div class="cuenta">
    <span>Mi cuenta</span>
    <span>Mis compras</span>
    <span>Cerrar sesión</span>
  </div>
{/if}

{#if imagenSeleccionada}
  <div class="image-container" on:click={() => imagenSeleccionada = null}>
    <img src={imagenSeleccionada} alt="Imagen seleccionada" />
  </div>
{/if}

<div class="product-list">
  {#each $carrito as producto}
    <div class="product">
      <div class="product-image" on:click={() => seleccionarImagen(producto.imagen)}>
        <img src={producto.imagen} alt={producto.nombre} />
      </div>
      <div class="product-info">
        <p class="descripcion">{producto.descripcion}</p>
        <h2>{producto.nombre}</h2>
        <p class="price">${producto.precio.toFixed(2)}</p>
      </div>
      <div class="product-actions">
        <button on:click={() => agregarAlCarrito(producto)}>
          🛒 {producto.cantidad > 0 ? 'Agregado' : 'Agregar al carrito'}
        </button>
        <div class="cantidad">
          <button class="minus" on:click={() => { if (producto.cantidad > 0) cambiarCantidad(producto, producto.cantidad - 1); }}>-</button>
          <span>{producto.cantidad}</span>
          <button class="plus" on:click={() => cambiarCantidad(producto, producto.cantidad + 1)}>+</button>
        </div>
      </div>
    </div>
  {/each}
</div>

<style>
  :global(body){
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
    background-color: #f9f9f9;
  }

  .menu {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 20px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    background-color: #fff;
  }

  .logo {
    font-size: 1.5em;
    font-weight: bold;
  }

  .menu-links {
    display: flex;
    list-style: none;
    gap: 20px;
    margin: 0;
    padding: 0;
  }

  .menu-links li a {
    text-decoration: none;
    color: #333;
    font-weight: bold;
    padding: 7px;
    border-radius: 10px;
  }

  .menu-links li a:hover {
    background: #d35400;
    color: #fcfbfb;
  }

  .menu-icons {
    display: flex;
    gap: 15px;
    font-size: 1.5em;
    cursor: pointer;
  }

  .carrito {
    position: relative;
  }

  .cart {
    position: absolute;
    top: 60px;
    right: 20px;
    width: 300px;
    background: #ffffff;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    padding: 15px;
    z-index: 10;
    overflow: hidden;
    max-height: 400px;
    overflow-y: auto;
  }

  .cart h1 {
    font-size: 1.4em;
    margin: 0 0 10px;
  }

  .producto-en-carrito {
    display: flex;
    gap: 15px;
    margin-bottom: 15px;
    align-items: center;
  }

  .producto-img {
    width: 50px;
    height: 50px;
    object-fit: cover;
    border-radius: 5px;
  }

  .producto-info {
    display: flex;
    justify-content: space-between;
    width: 100%;
    align-items: center;
  }

  .producto-texto {
    flex-grow: 1;
  }

  .producto-nombre {
    font-weight: bold;
  }

  .producto-precio {
    color: #d35400;
    font-weight: bold;
  }

  .eliminar {
    background-color: #e74c3c;
    color: white;
    border: none;
    border-radius: 5px;
    padding: 5px 10px;
    cursor: pointer;
  }

  .eliminar:hover {
    background-color: #c0392b;
  }

  .cuenta {
    position: absolute;
    top: 60px;
    right: 20px;
    width: 300px;
    display: flex;
    flex-direction: column;
    background: #ffffff;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    padding: 15px;
    z-index: 10;
    gap: 5px;
  }

  .cuenta span {
    padding: 10px 0 10px 10px;
    color: #666;
    font-size: 0.9em;
    border-radius: 5px;
    cursor: pointer;
  }

  .cuenta span:hover {
    background: #f4f5f9;
  }

  .product-list {
    display: flex;
    width: 100%;
    justify-content: center;
    flex-wrap: wrap;
    gap: 30px;
    padding: 40px 0 40px 0;
  }

  .product {
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 10px;
    background: #fff;
    width: 230px;
    height: max-content;
    text-align: center;
  }
  .product-image{
    overflow: hidden;
  }
  .product-image img {
    width: 100%;
    height: 160px;
    object-fit: cover;
    border-radius: 5px;
    cursor: pointer;
    transition: transform 0.3s ease-in-out;
  }
  .product-image img:hover{
    transform: scale(1.2);
  }
  .product-info {
    margin-top: 10px;
  }

  .descripcion {
    font-size: 0.9em;
    color: #888;
  }

  .price {
    color: #d35400;
    font-weight: bold;
    margin-top: 10px;
  }

  .product-actions {
    margin-top: 10px;
  }

  .product-actions button {
    background-color: #d35400;
    color: white;
    padding: 8px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    width: 100%;
  }

  .product-actions button:hover {
    background-color: #c0392b;
  }

  .cantidad {
    display: flex;
    gap: 10px;
    justify-content: center;
    margin-top: 10px;
  }

  .cantidad button {
    border: none;
    padding: 10px;
    font-size: 16px;
    cursor: pointer;
    border-radius: 5px;
    background-color: #3498db; 
    color: white;
  }

  .cantidad button:hover {
    background-color: #2980b9; 
  }

  .image-container {
    position: fixed; 
    top: 0;
    left: 0;
    width: 100vw; 
    height: 100vh; 
    background-color: rgba(0, 0, 0, 0.5); 
    display: flex; 
    justify-content: center; 
    align-items: center; 
    z-index: 100; 
  }

  .image-container img {
    max-width: 90%; 
    max-height: 90%; 
    object-fit: contain; 
  }
</style>
