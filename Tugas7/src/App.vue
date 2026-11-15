
<template>
  <div>
    <nav>
      <router-link to="/">Beranda</router-link>
      |
      <router-link to="/cart">Keranjang Belanja</router-link>
    </nav>

    <router-view />
  </div>
</template>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f5f5f5;
}

nav {
  background: #42b883;
  padding: 20px;
}

nav a {
  color: white;
  text-decoration: none;
  font-weight: bold;
  margin: 10px;
}
</style>
