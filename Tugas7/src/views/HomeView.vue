
<script setup>
import ProductCard from '../components/ProductCard.vue'
import { useCartStore } from '../stores/cart'

const cartStore = useCartStore()

const products = [
  {
    id: 1,
    name: 'Laptop',
    description: 'Laptop untuk belajar dan bekerja',
    price: 5000000
  },
  {
    id: 2,
    name: 'Mouse',
    description: 'Mouse wireless berkualitas',
    price: 150000
  },
  {
    id: 3,
    name: 'Keyboard',
    description: 'Keyboard mechanical',
    price: 350000
  }
]

function buyProduct(product) {
  cartStore.addToCart(product)
  alert(product.name + ' berhasil ditambahkan ke keranjang!')
}
</script>

<template>
  <div class="container">
    <h1>Katalog Produk</h1>

    <p>
      Selamat datang di toko online sederhana.
    </p>

    <div class="products">
      <ProductCard
        v-for="product in products"
        :key="product.id"
        :product="product"
        @buy="buyProduct"
      />
    </div>
  </div>
</template>

<style scoped>
.container {
  padding: 30px;
}

.products {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}
</style>
