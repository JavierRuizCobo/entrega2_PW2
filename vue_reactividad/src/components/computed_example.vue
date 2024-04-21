<template>
  <h1>Carrito de compras con computed</h1>
  <div>
    <h2>Carrito de compras</h2>
    <ul>
      <li v-for="(product, index) in shoppingCart" :key="index">
        {{ product.name }} - {{ product.quantity }} x {{ product.price | formatoMoneda }} 
        <button @click="removeProduct(index)">Eliminar</button>
      </li>
    </ul>
    <h3>Productos disponibles</h3>
    <ul>
      <li v-for="(producto, index) in products" :key="index">
        {{ producto.name }} - {{ producto.price | formatoMoneda }}
        <input type="number" v-model.number="producto.quantity" min="0" max="10" placeholder="Cantidad">
        <button @click="addProduct(index)">Agregar</button>
      </li>
    </ul>
    <p>Total: {{ total | formatoMoneda }}</p>
  </div>
</template>

<script setup>
  import {reactive, computed } from 'vue';

  const shoppingCart = reactive([]);
  const products = reactive([
    { name: 'Camisa', price: 20, quantity: 0 },
    { name: 'Pantalón', price: 30, quantity: 0 },
    { name: 'Zapatos', price: 50, quantity: 0 }
  ]);

  // Propiedad computada para calcular el precio total del carrito
  const total = computed(() => {
    return shoppingCart.reduce((total, product) => total + (product.price * product.quantity), 0);
  });


  function formatoMoneda(valor){
    return `$ ${valor.toFixed(2)}`;
  };

  function addProduct(index){
    const product = products[index];
    if (product.quantity > 0) {
      shoppingCart.push({ name: product.name, price: product.price, quantity: product.quantity });
      product.quantity = 0;
    }
  };

  function removeProduct(index){
    shoppingCart.splice(index, 1);
  };

</script>
