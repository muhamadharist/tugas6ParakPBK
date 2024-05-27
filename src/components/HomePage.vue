<template>
    <div>
      <h1>Selamat Datang di Toko Sepeda Motor</h1>
      <div v-for="product in products" :key="product.id">
        <ProductCard :product="product" />
      </div>
    </div>
  </template>
  
  <script>
  import ProductCard from '@/components/ProductCard.vue'; // Pastikan path-nya sesuai
  
  export default {
    name: 'HomePage',
    components: {
      ProductCard
    },
    props: {
      products: Array
    }
  }
  </script>
  
  <style scoped>
  /* Gaya khusus untuk halaman beranda dapat ditambahkan di sini */
  </style>
  