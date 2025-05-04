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

const addTodo = () => {
  if (
    input_course.value.trim() === '' ||
    input_task.value.trim() === '' ||
    input_category.value === null ||
    input_deadline.value === ''
  ) return

  todos.value.push({
    course: input_course.value,
    task: input_task.value,
    category: input_category.value,
    deadline: input_deadline.value,
    done: false,
    createdAt: new Date().getTime()
  })

  input_course.value = ''
  input_task.value = ''
  input_category.value = null
  input_deadline.value = ''
}

const removeTodo = todo => {
  todos.value = todos.value.filter(t => t !== todo)
}

watch(todos, newVal => {
  localStorage.setItem('todos', JSON.stringify(newVal))
}, { deep: true })

watch(name, newVal => {
  localStorage.setItem('name', newVal)
})

onMounted(() => {
  name.value = localStorage.getItem('name') || ''
  todos.value = JSON.parse(localStorage.getItem('todos')) || []
})

const todos_asc = computed(() => {
  return [...todos.value].sort((a, b) => b.createdAt - a.createdAt)
})

const filteredTodos = computed(() => {
  if (showOnlyUndone.value) {
    return todos_asc.value.filter(todo => !todo.done)
  }
  return todos_asc.value
})

</script>

<template>
  <div class="container">
    <main class="app">
      <section class="greeting">
        <h2 class="title">Selamat Datang Dr.Jefry</h2>
      </section>

      <section class="create-todo">
        <h3>Ada Tugas Apa Hari Ini?</h3>

        <form @submit.prevent="addTodo">
          <h4>Mata Kuliah</h4>
          <select v-model="input_course">
            <option value="" disabled selected>Pilih Mata Kuliah</option>
            <option v-for="course in courseOptions" :key="course" :value="course">{{ course }}</option>
          </select>

          <h4>Tugas / Materi</h4>
          <input type="text" placeholder="Contoh: P8 - Membuat Sistem Todo List" v-model="input_task" />

          <h4>Kategori</h4>
          <div class="options">
            <label>
              <input type="radio" name="category" value="teori" v-model="input_category" />
              <span class="bubble teori"></span>
              <div>Teori</div>
            </label>

            <label>
              <input type="radio" name="category" value="pratikum" v-model="input_category" />
              <span class="bubble pratikum"></span>
              <div>Pratikum</div>
            </label>
          </div>

          <h4>Batas Waktu</h4>
          <input type="date" v-model="input_deadline" />

          <input type="submit" value="Tambahkan" />
        </form>
      </section>
      </main>
      </div>
</template>
