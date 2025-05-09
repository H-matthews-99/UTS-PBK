<script setup>import { ref, computed } from 'vue'

const komikBaru = ref('')
const komikList = ref([
  { id: 1, judul: 'One Piece', dibaca: false },
  { id: 2, judul: 'Naruto', dibaca: true },
  { id: 3, judul: 'Attack on Titan', dibaca: false }
])
const filterBelumDibaca = ref(false)

function tambahKomik() {
  if (komikBaru.value.trim()) {
    komikList.value.push({
      id: Date.now(),
      judul: komikBaru.value,
      dibaca: false
    })
    komikBaru.value = ''
  }
}

function hapusKomik(id) {
  komikList.value = komikList.value.filter(k => k.id !== id)
}

  const komikDitampilkan = computed(() =>
  filterBelumDibaca.value
    ? komikList.value.filter(k => !k.dibaca)
    : komikList.value)

</script>



<template>
  <div class="container">
    <h1>📚 Daftar Komik</h1>

    <div class="form">
      
      <input
  v-model="komikBaru"
  placeholder="Masukkan judul komik"
  style="
    width: 80%;
    padding: 12px 16px;
    font-size: 16px;
    font-family: Arial, sans-serif;
    color: #333;
    background-color: #fffbe6;
    border: 2px solid #ddd;
    border-radius: 10px;
    box-sizing: border-box;
    transition: border-color 0.3s ease, box-shadow 0.3s ease;

  "
/>
<button @click="tambahKomik">Tambah</button>
    </div>

    <div class="filter">
      <label>
        <input type="checkbox" v-model="filterBelumDibaca" />
        Tampilkan hanya yang belum dibaca
      </label>
    </div>

    <ul class="komik-list">
      <li v-for="komik in komikDitampilkan" :key="komik.id" class="komik-card">
        <input type="checkbox" v-model="komik.dibaca" />
        <span :class="{ selesai: komik.dibaca }">{{ komik.judul }}</span>
        <button @click="hapusKomik(komik.id)">Hapus</button>
      </li>
    </ul>
  </div>
 
</template>


<style scoped>
.container {
  max-width: 600px;
  margin: 2rem auto;
  padding: 2rem;
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg, #fceabb, #f8b500);
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.1);
  color: #333;
  transition: box-shadow 0.3s ease, transform 0.3s ease;
}

.container:hover {
  box-shadow: 0 12px 32px rgba(0, 0, 0, 0.15);
  transform: translateY(-4px);
}

/* Input field */
input[type="text"],
input[type="checkbox"],
input[type="email"] {
  font-size: 16px;
  font-family: inherit;
}

/* Text Input */
.form input[type="text"] {
  width: calc(100% - 120px);
  padding: 12px 16px;
  border: 2px solid #ddd;
  border-radius: 8px;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
  box-sizing: border-box;
  margin-right: 10px;
}

.form input[type="text"]:focus {
  border-color: #e5a700;
  box-shadow: 0 0 8px rgba(248, 181, 0, 0.3);
  outline: none;
}

/* Button */
button {
  padding: 12px 20px;
  background-color: #f8b500;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

button:hover {
  background-color: #e5a700;
  transform: translateY(-2px);
}

button:active {
  background-color: #d68a00;
  transform: translateY(2px);
}

/* Checkbox styling */
input[type="checkbox"] {
  width: 20px;
  height: 20px;
  accent-color: #f8b500;
  cursor: pointer;
  margin-right: 10px;
}

/* Komik card styling */
.komik-list {
  list-style: none;
  padding: 0;
  margin-top: 20px;
}

.komik-card {
  background-color: white;
  border-radius: 8px;
  padding: 12px;
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
  transition: background-color 0.3s ease;
}

.komik-card:hover {
  background-color: #fff5d1;
}

.komik-card .selesai {
  text-decoration: line-through;
  color: #888;
}

/* Filter section */
.filter {
  margin: 20px 0;
  font-size: 16px;
}






</style>