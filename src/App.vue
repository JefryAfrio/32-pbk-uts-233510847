<script setup>
import { ref, onMounted, computed, watch } from 'vue'

const todos = ref([])
const name = ref('')

const input_course = ref('')
const input_task = ref('')
const input_category = ref(null)
const input_deadline = ref('')

const showOnlyUndone = ref(false)

const courseOptions = [
  'Desain dan Analis Algoritma',
  'Elektronika Digital',
  'Grafika Komputer',
  'Jaringan Komputer',
  'Pemograman Berorientasi Objek',
  'Pemograman Berbasis Komponen',
  'Matematika Diskrit',
  'Interkasi Manusia dan Komputer',
]
</script>

<template>
  
</template>
