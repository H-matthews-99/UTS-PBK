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

 
</template>


<style scoped>

</style>