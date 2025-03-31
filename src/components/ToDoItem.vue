<template>
  <li>
    <input placeholder="Введи имя"
           type="text"
           v-model="name"
    >
    <input placeholder="Задача"
           type="text"
           v-model="task"
    >
    <button @click="onSave">Сохранить</button>
    <button @click="onDelete">Удалить</button>
  </li>
</template>

<script setup>
import {ref} from "vue";
const props = defineProps({
  name: {
    type: String,
    default: ''
  },
  task: {
    type: String,
    default: ''
  }
})
const emit = defineEmits(['delete','save'])

const name = ref(props.name)
const task = ref(props.task)

function onDelete() {
  emit('delete')
}
function onSave() {
  emit('save',{
    name: name.value,
    task: task.value,
  })
}
</script>

<style scoped>

</style>

