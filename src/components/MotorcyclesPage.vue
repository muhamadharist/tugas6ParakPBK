<template>
    <div>
      <h1>Sepeda Motor</h1>
      <div v-for="product in products" :key="product.id">
        <ProductCard :product="product" />
      </div>
    </div>
  </template>
  
  <script>
  import ProductCard from '@/components/ProductCard.vue'; // Pastikan path-nya sesuai
  
  export default {
    name: 'MotorcyclesPage',
    components: {
      ProductCard
    },
    props: {
      products: Array
    }
  }
  </script>
  
  <style scoped>
  /* Gaya khusus untuk halaman sepeda motor dapat ditambahkan di sini */
  </style>
  