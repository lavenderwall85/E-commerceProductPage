<script>
  // Lógica del menú
  let carritoVisible = false;
  let cuenta = false;
  let selectedImage = null;
  

  // logica lista productos

  let products = [
    
    { id: 1, name: 'Running Sneakers', price: 75.00, image: '/images/zapatosHombres/modelo1.jpg', description: 'Comfortable running shoes', added: false },
    { id: 2, name: 'Casual Sneakers', price: 60.00, image: '/images/zapatosHombres/modelo2.jpg', description: 'Stylish casual shoes', added: false },
    { id: 3, name: 'High-Top Sneakers', price: 85.00, image: '/images/zapatosHombres/modelo3.jpg', description: 'Trendy high-top design', added: false },
    { id: 4, name: 'High-Top Sneakers', price: 85.00, image: '/images/zapatosHombres/modelo4.jpg', description: 'Trendy high-top design', added: false },
    { id: 5, name: 'High-Top Sneakers', price: 85.00, image: '/images/zapatosHombres/modelo5.jpg', description: 'Trendy high-top design', added: false },
    { id: 6, name: 'High-Top Sneakers', price: 85.00, image: '/images/zapatosHombres/modelo6.jpg', description: 'Trendy high-top design', added: false },
    { id: 7, name: 'High-Top Sneakers', price: 85.00, image: '/images/zapatosHombres/modelo7.jpg', description: 'Trendy high-top design', added: false }
  ];
  

  function toggleCarrito() {
    carritoVisible = !carritoVisible;
  }

  function toggleCuenta() {
    cuenta = !cuenta;
  }

  function addToCart(product) {
    product.added = !product.added;
  }

  function selectImage(image) {
    selectedImage = image; // Actualiza la imagen seleccionada
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

{#if selectedImage}
  <div class="image-container" on:click={() => selectedImage = null}>
    <img src={selectedImage} alt="Selected Product" />
  </div>
{/if}

  <div class="product-list">
    {#each products as product}
      <div class="product">
        <div class="product-image" on:click={() => selectImage(product.image)}>
          <img src={product.image} alt={product.name} />
        </div>
        <button on:click={() => addToCart(product)}>
          🛒 {product.added ? 'Added' : 'Add to Cart'}
        </button>
        <div class="product-info">
          <p class="description">{product.description}</p>
          <h2>{product.name}</h2>
          <p class="price">${product.price.toFixed(2)}</p>
        </div>
      </div>
    {/each}
  </div>



<style>
  :global(body){
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
    overflow-y: auto;
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
  /*lista de productos*/
  .product-list {
    display: flex;
    width: 100%;
    justify-content: center;
    flex-wrap: wrap;
    gap: 30px;
    padding: 40px 0 40px 0;
    background: #f9f9f9;
    height: 100%;
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
  
  .product-image img {
    width: 100%;
    height: auto;
    border-radius: 8px;
    transition: transform 0.2s;
  }
  .product-image img:hover{
    cursor: pointer;
    transform: scale(1.1);

  }
 
  .product-image img::hover button{
    margin-top: 20px;
  }

  button {
    margin: 10px 0;
    padding: 5px 10px;
    background: #ff7f50;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  button:hover {
    background: #e67348;
  }

  .product-info p {
    margin: 5px 0;
  }

  .description {
    font-size: 0.9em;
    color: #777;
  }

  .price {
    font-size: 1.1em;
    color: #d35400;
  }

  .image-container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.8);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 10; 
  }

  .image-container img {
    max-width: 80%;
    max-height: 80%;
    border-radius: 8px;
  }
</style>
