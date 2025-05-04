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

</script>

<template>

</template>
