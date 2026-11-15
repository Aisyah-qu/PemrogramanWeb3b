
<script setup>
import { useCartStore } from '../stores/cart'

const cartStore = useCartStore()
</script>

<template>
  <div class="container">
    <h1>Keranjang Belanja</h1>

    <p v-if="cartStore.items.length === 0">
      Keranjang masih kosong.
    </p>

    <div v-else>
      <div
        v-for="item in cartStore.items"
        :key="item.id"
        class="cart-item"
      >
        <h3>{{ item.name }}</h3>

        <p>
          Harga: Rp {{ item.price.toLocaleString('id-ID') }}
        </p>

        <p>Jumlah: {{ item.quantity }}</p>

        <p>
          Subtotal:
          Rp {{ (item.price * item.quantity).toLocaleString('id-ID') }}
        </p>

        <button @click="cartStore.removeFromCart(item.id)">
          Hapus
        </button>
      </div>

      <h3>Total Barang: {{ cartStore.totalItems }}</h3>

      <h2>
        Total Harga:
        Rp {{ cartStore.totalPrice.toLocaleString('id-ID') }}
      </h2>
    </div>
  </div>
</template>

<style scoped>
.container {
  padding: 30px;
}

.cart-item {
  border: 1px solid #ddd;
  padding: 15px;
  margin-bottom: 15px;
  border-radius: 10px;
}

button {
  background: #e74c3c;
  color: white;
  border: none;
  padding: 8px 15px;
  border-radius: 5px;
  cursor: pointer;
}
</style>
