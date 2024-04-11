<script>
  let temperature = 25; // Temperatura en grados Celsius

	function increment() {
    temperature += 5;
  }
  // Si la temperatura supera los 30 grados, consideramos que hace calor
  $: isHot = temperature > 30;

	let product = { name: 'Mazda 3', price: 23000 };
  let discount = 10; // Descuento en porcentaje

  // Calculamos el precio con descuento
	$: if (discount <= 100 && discount >= 0) {
				product.discountedPrice = product.price * (1 - discount / 100);
	  } else {
				product.discountedPrice = product.price * (1 - 0 / 100);
		}

</script>

<h1>Ejemplo 1</h1>
<div class="box">
  <p>Temperatura: <b>{temperature}°C</b></p>
	<button on:click={increment}>
		+5
</button>
  {#if isHot}
    <p><b>Hace calor 🔥</b></p>
  {:else}
    <p><b>No hace tanto calor</b></p>
  {/if}
</div>

<h1>Ejemplo 2</h1>
<div class="box">
  <p>Producto: <b>{product.name}</b></p>
  <p>Precio original: <b>{product.price} €</b></p>
	<label for="discountInput">Introduce el descuento (%):</label>
  <input type="number" id="discountInput" min="0" max="100" step="1" bind:value={discount}>
  <p>Precio con descuento: <b>{product.discountedPrice.toFixed(2)} €</b></p>
</div>


<style>

  .box {
    display: flex;
    flex-direction: column;
    align-items: center;
    background: linear-gradient(to right, #ff7e5f, #feb47b);
    padding: 20px;
    margin-bottom: 20px;
    border-radius: 8px;
    color: #fff;
  }

	input {
	  margin-top: 10px;
	  padding: 8px;
	  border: none;
	  border-radius: 4px;
	  outline: none;
	  width: max-content;
	}
	
  button {
    width: max-content;
    padding: 10px 20px;
    background-color: #2d4059;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }

  button:hover {
    background-color: #1b262c;
  }
</style>


