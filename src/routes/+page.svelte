<script>
  import { writable } from 'svelte/store';

  // Store para la cantidad en el carrito
  export const cantidadCarrito = writable(0);

  let subtitulo = 'Fall Limited Edition Sneakers';
  let titulo = 'Sneaker Company';
  let titulocart = 'Fall Limited Edition Sneakers';
  let descripcion = 'These low-profile sneakers are your perfect casual wear companion. Featuring a durable rubber outer sole they withstand everything the weather can offer';
  let precio = 125;
  let descuento = 50;
  let precioOriginal = 250;
  let cantidad = 1;
  let imgPrincipal = '/images/image-product-1.jpg';
  let imgExtra1 = '/images/image-product-1-thumbnail.jpg';
  let imgExtra2 = '/images/image-product-2-thumbnail.jpg';
  let imgExtra3 = '/images/image-product-3-thumbnail.jpg';
  let carritoVisible = false;  

  function toggleCarrito() {
    carritoVisible = !carritoVisible;
  }

  function agregarAlCarrito() {
    cantidadCarrito.update(n => n + cantidad);
  }

  function actualizarCantidad(operacion) {
    if (operacion === 'sumar') {
      cantidad++;
    } else if (operacion === 'restar' && cantidad > 1) {
      cantidad--;
    }
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
    <span class="carrito" on:click={toggleCarrito}>🛒</span> 
    <span class="avatar">👤</span>
  </div>
</nav>

<main>
  {#if carritoVisible}
    <div class="cart">
      <h1>cart</h1>
      <div class="infocart">
        <img src={imgExtra1} alt="">
        <div class="moreinfo">
          <h1>{titulocart}</h1>
          <h2> $125 X <span>{$cantidadCarrito}</span> <span>${125 * $cantidadCarrito}</span></h2>
        </div>
        <i>🚮</i>
      </div>
      <button class="comprar">Checkout</button>
    </div>
  {/if}

  <div class="contenedor">
    <div class="imagen-principal">
      <img src={imgPrincipal} alt="imagen principal">
      <div class="imagenes-extra">
        <img src={imgExtra1} alt="imagen extra 1">
        <img src={imgExtra2} alt="imagen extra 2">
        <img src={imgExtra3} alt="imagen extra 3">
      </div>
    </div>

    <div class="info-producto">
      <h3>{titulo}</h3>
      <h1>{subtitulo}</h1>
      <p>{descripcion}</p>
      <h2>${precio} <span class="descuento">{descuento}%</span></h2>
      <p class="precio-original">${precioOriginal}</p>

      <div class="acciones">
        <div class="cantidad">
          <button on:click={() => actualizarCantidad('restar')}>-</button>
          <span>{cantidad}</span>
          <button on:click={() => actualizarCantidad('sumar')}>+</button>
          <button class="agregar-carrito" on:click={agregarAlCarrito}>🛒 Añadir al carrito</button>
        </div>
      </div>
    </div>
  </div>
</main>
  
<style>
  :global(body){
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
    overflow-y: hidden;
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

  .menu-links li a:hover{
    background: #d35400;
    color: #fcfbfb;
  }

  .menu-links li a {
    text-decoration: none;
    color: #333;
    font-weight: bold;
    padding: 7px;
    border-radius: 10px;
  }

  .menu-icons {
    display: flex;
    gap: 15px;
    font-size: 1.5em;
    cursor: pointer;
  }

  main {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    min-height: 100vh;
    background-color: #f9f9f9;
  }

  .cart {
    display: block;
    position: absolute;
    top: 20px;
    right: 20px;
    width: 320px;
    background: #ffffff;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    padding: 15px 0;
    z-index: 10;
    transition: all 0.3s ease;
  }

  .cart h1 {
    font-size: 1.4em;
    font-weight: bold;
    text-align: left;
    margin: 0 0 10px 15px;
    color: #333;
  }

  .cart .infocart {
    display: flex;
    width: 100%;
    margin-top: 15px;
    border-top: #ddd 1px solid;
    padding: 12px 10px;
    align-items: center;
    gap: 15px;
  }

  .cart .infocart img {
    width: 50px;
    height: 50px;
    border-radius: 8px;
  }

  .cart .infocart .moreinfo {
    display: flex;
    flex-direction: column;
  }

  .cart .moreinfo h1 {
    font-size: 0.9em;
    font-weight: 500;
    margin-left: 0;
    color: #444;
  }

  .cart .moreinfo h2 {
    font-size: 0.9em;
    color: #777;
    margin: 5px 0;
  }

  .cart .infocart i {
    margin: 0 20px 0 0;
    cursor: pointer;
    font-size: 1.5em;
    color: #e67e22;
    transition: color 0.2s ease;
  }

  .cart .infocart i:hover {
    color: #c0392b;
  }

  .cart .comprar {
    display: block;
    width: calc(100% - 30px);
    margin: 15px auto;
    padding: 10px;
    background-color: #e67e22;
    color: white;
    border: none;
    border-radius: 5px;
    text-align: center;
    font-size: 1em;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .cart .comprar:hover {
    background-color: #d35400;
  }

  .contenedor {
    display: flex;
    flex-direction: row;
    max-width: 800px;
    background: white;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    overflow: hidden;
  }

  .imagen-principal {
    flex: 1;
    padding: 10px;
  }

  .imagen-principal img {
    width: 100%;
    border-radius: 5px;
  }

  .imagenes-extra {
    display: flex;
    justify-content: center;
    gap: 10px;
    margin-top: 10px;
  }

  .imagenes-extra img {
    width: 70px;
    height: 70px;
    border: 1px solid #ddd;
    border-radius: 5px;
    cursor: pointer;
    transition: transform 0.2s;
  }

  .imagenes-extra img:hover {
    transform: scale(1.1);
  }

  .imagenes-extra:hover img:not(:hover) {
    filter: blur(1.7px);
  }

  .info-producto {
    flex: 1;
    padding: 20px;
  }

  .info-producto h3{
    text-transform: uppercase;
    font-size: 0.9em;
    font-weight: 400;
  }

  .info-producto h1 {
    font-size: 1.7em;
    margin-bottom: 10px;
  }

  .info-producto p {
    font-size: 1em;
    margin-bottom: 15px;
    color: #666;
  }

  .info-producto h2 {
    color: #e67e22;
    margin-bottom: 5px;
  }

  .descuento {
    background: #484747;
    color: #f2efef;
    padding: 3px 5px;
    font-size: 0.8em;
    border-radius: 5px;
  }

  .precio-original {
    text-decoration: line-through;
    color: #999;
  }

  .acciones {
    display: flex;
    gap: 10px;
    align-items: center;
  }

  .cantidad button {
    padding: 5px 10px;
    background-color: #e67e22;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .cantidad button:hover {
    background-color: #d35400;
  }

  .agregar-carrito {
    padding: 10px 20px;
    background-color: #e67e22;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .agregar-carrito:hover {
    background-color: #d35400;
  }
</style>
