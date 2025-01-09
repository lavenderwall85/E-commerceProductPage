<script>
  // Lógica del menú
  let carritoVisible = false;
  let cuenta = false;

  function toggleCarrito() {
    carritoVisible = !carritoVisible;
  }

  function toggleCuenta() {
    cuenta = !cuenta;
  }
</script>

<nav class="menu">
  <div class="logo" href="/routes">sneakers</div>
  <ul class="menu-links">
    <li><a href="/Home">Colecciones</a></li>
    <li><a href="/Hombres">Hombres</a></li>
    <li><a href="/Mujeres">Mujeres</a></li>
    <li><a href="/AcercaDe">Acerca de</a></li>
    <li><a href="/Contacto">Contacto</a></li>
  </ul>
  <div class="menu-icons">
    <span class="carrito" on:click={toggleCarrito}>🛒</span>
    <span class="avatar" on:click={toggleCuenta}>👤</span>
  </div>
</nav>

{#if carritoVisible}
  <div class="cart">
    <h1>Cart</h1>
    <p>Tu carrito está vacío.</p>
  </div>
{/if}

{#if cuenta}
<div class="cuenta">
  <span>Mi cuenta</span>
  <span>Mis compras</span>
  <span>Cerrar sesion</span>
</div>
{/if}

<style>
  :global(body){
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
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

  .menu-links li a:hover{
    background: #d35400;
    color: #fcfbfb;
  }

  .menu-icons {
    display: flex;
    gap: 15px;
    font-size: 1.5em;
    cursor: pointer;
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
  }

  .cart h1 {
    font-size: 1.4em;
    margin: 0 0 10px;
  }

  .cart p {
    font-size: 1em;
    color: #666;
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

  .cuenta span{
    padding: 10px 0 10px 10px;
    color: #666;
    font-size: 0.9em;
    border-radius: 5px;
    cursor: pointer;
  }

  .cuenta span:hover{
    background: #f4f5f9;
  }
</style>
