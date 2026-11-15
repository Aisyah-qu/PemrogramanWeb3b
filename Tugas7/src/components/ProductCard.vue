
<script setup>
defineProps({
  product: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['buy'])
</script>

<template>
  <div class="product-card">
    <h3>{{ product.name }}</h3>
    <p>{{ product.description }}</p>
    <h4>Rp {{ product.price.toLocaleString('id-ID') }}</h4>

    <button @click="$emit('buy', product)">
      Beli Sekarang
    </button>
  </div>
</template>

<style scoped>
.product-card {
  border: 1px solid #ddd;
  padding: 20px;
  border-radius: 10px;
  width: 220px;
  background: white;
}

button {
  background: #42b883;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
}
</style>
