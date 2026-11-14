
<script setup>
import { ref, computed } from 'vue'

// Data input buku
const judul = ref('')
const kategori = ref('Novel')
const statusBaca = ref(false)

// Daftar buku
const daftarBuku = ref([])

// Fungsi tambah buku
function tambahBuku() {
  if (judul.value.trim() === '') {
    alert('Judul buku harus diisi!')
    return
  }

  daftarBuku.value.push({
    id: Date.now(),
    judul: judul.value,
    kategori: kategori.value,
    selesai: statusBaca.value
  })

  judul.value = ''
  kategori.value = 'Novel'
  statusBaca.value = false
}

// Menghitung buku yang selesai dibaca
const jumlahSelesai = computed(() => {
  return daftarBuku.value.filter(buku => buku.selesai).length
})
</script>


<template>
  <div class="container">
    <header class="header">
      <h1>📚 Aplikasi Buku Catatan</h1>
      <p>Catat buku favoritmu, jadi lebih teratur!</p>
    </header>

    <section class="card">
      <h2>➕ Tambah Buku</h2>

      <form @submit.prevent="tambahBuku">
        <label>Judul Buku</label>
        <input
          v-model="judul"
          type="text"
          placeholder="Masukkan judul buku..."
        />

        <label>Kategori Buku</label>
        <select v-model="kategori">
          <option value="Novel">Novel</option>
          <option value="Pendidikan">Pendidikan</option>
          <option value="Komik">Komik</option>
          <option value="Biografi">Biografi</option>
        </select>

        <label class="check">
          <input type="checkbox" v-model="statusBaca" />
          Sudah selesai dibaca
        </label>

        <button type="submit">+ Tambah Buku</button>
      </form>
    </section>

    <section class="card">
      <h2>📖 Daftar Buku</h2>

      <div class="jumlah">
        Jumlah buku selesai dibaca:
        <strong>{{ jumlahSelesai }}</strong>
      </div>

      <ul v-if="daftarBuku.length > 0">
        <li v-for="buku in daftarBuku" :key="buku.id">
          <div>
            <strong>{{ buku.judul }}</strong>
            <span>{{ buku.kategori }}</span>
          </div>

          <span :class="buku.selesai ? 'selesai' : 'belum'">
            {{ buku.selesai ? '✓ Sudah dibaca' : '○ Belum dibaca' }}
          </span>

          <input
            type="checkbox"
            v-model="buku.selesai"
            title="Ubah status baca"
          />
        </li>
      </ul>

      <p v-else class="kosong">
        📚 Belum ada buku. Yuk tambahkan buku!
      </p>
    </section>
  </div>
</template>


<style scoped>
* {
  box-sizing: border-box;
}

.container {
  max-width: 850px;
  margin: 35px auto;
  padding: 20px;
  font-family: Arial, sans-serif;
  color: #35254e;
}

.header {
  background: linear-gradient(135deg, #e8d5ff, #f9d9ef);
  padding: 30px;
  border-radius: 20px;
  text-align: center;
  margin-bottom: 25px;
}

.header h1 {
  color: #59358c;
  margin: 0 0 10px;
}

.header p {
  margin: 0;
  color: #765b91;
}

.card {
  background: white;
  padding: 25px;
  border-radius: 18px;
  margin-bottom: 22px;
  box-shadow: 0 4px 15px rgba(100, 65, 140, 0.12);
}

h2 {
  color: #7046a5;
  margin-top: 0;
}

label {
  display: block;
  margin: 15px 0 7px;
  font-weight: bold;
}

input[type="text"],
select {
  width: 100%;
  padding: 12px;
  border: 1px solid #d9c8ec;
  border-radius: 10px;
  font-size: 15px;
}

.check {
  display: flex;
  align-items: center;
  gap: 8px;
}

button {
  background: #8962bd;
  color: white;
  padding: 12px 22px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  margin-top: 12px;
}

button:hover {
  background: #7046a5;
}

.jumlah {
  background: #f0e5ff;
  padding: 14px;
  border-radius: 10px;
  margin: 15px 0;
  color: #59358c;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  padding: 15px 5px;
  border-bottom: 1px solid #eee4f5;
  flex-wrap: wrap;
}

li strong {
  display: block;
  margin-bottom: 7px;
}

li div span {
  font-size: 13px;
  color: #8962bd;
}

.selesai {
  color: #27834c;
  background: #e1f5e7;
  padding: 7px 10px;
  border-radius: 15px;
}

.belum {
  color: #777;
  background: #eee;
  padding: 7px 10px;
  border-radius: 15px;
}

.kosong {
  text-align: center;
  padding: 25px;
  background: #f5edff;
  border-radius: 12px;
  color: #765b91;
}
</style>
