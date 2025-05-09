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
 
</template>


<style scoped>

</style>