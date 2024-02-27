<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
const produtos = ref([]);

onMounted(async () => {
  const response = await axios.get('https://fakestoreapi.com/products');
  produtos.value = response.data;
});

const formatPrice = (price) => `R$ ${price.toFixed(2).replace('.', ',')}`;
</script>

<template>
    <div>
      <h1>Produtos</h1>
      <div class="container">
        <div class="card" v-for="produto in produtos" :key="produto.id">
          <h1 class="card--title">{{ produto.title }}</h1>
          <p>{{ produto.description }}</p>
          <p>{{ formatPrice(produto.price) }}</p>
          <img class="card--avatar" :src="produto.image" :alt="produto.title" />
        </div>
      </div>
    </div>
  </template>
  