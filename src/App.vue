<template>
  <button @click="addToDoItem">Добавить задачу</button>
  <ul>
      <ToDoItem v-for="toDoItem in list"
                :key="toDoItem.id"
                :name="toDoItem.name"
                :task="toDoItem.task"
                @delete="deleteToDoItem(toDoItem.id)"
                @save="updateItem(toDoItem.id,$event)"
      >
      </ToDoItem>
  </ul>
</template>

<script setup>
import {ref, onMounted} from 'vue'
import ToDoItem from "./components/ToDoItem.vue";
const list = ref([])
const localStorageKey = 'to-do-storage'

function addToDoItem() {
  const toDoItem = {
    id: Date.now(),
    name: '',
    task: '',
  }
  list.value.push(toDoItem)
  updateLocalStorage()
}
function deleteToDoItem(id) {
  const result = list.value.filter((item) => item.id !== id)
  list.value = result
  updateLocalStorage()
}
function updateItem(id,newItem) {
  const item = list.value.find(item => item.id === id)
  item.name = newItem.name
  item.task = newItem.task
  updateLocalStorage()
}

function updateLocalStorage() {
  const stringifyList = JSON.stringify(list.value)
  localStorage.setItem(localStorageKey,stringifyList)
}

onMounted(()=> {
  const toDoItemsJson = localStorage.getItem(localStorageKey)
  const toDoItems = JSON.parse(toDoItemsJson)
  list.value = toDoItems || []
})
</script>

