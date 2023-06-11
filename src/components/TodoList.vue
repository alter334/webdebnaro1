<script setup lang="ts">
import { ref } from 'vue'
interface Task {
  name: string
  todo: boolean
  tasknum: number
}

const tasks = ref<Task[]>([])

const newTaskName = ref('')
const taskNum = ref<number>(0)
const addTask = () => {
  if (newTaskName.value.length != 0) {
    tasks.value.push({ name: newTaskName.value, todo: false, tasknum: taskNum.value })
    taskNum.value++
  }
  newTaskName.value = ''
}

const Switch = (switchnum: number) => {
  tasks.value[switchnum].todo = !tasks.value[switchnum].todo
}
</script>

<template>
  <div>
    <div>TodoList</div>
    <div>未完タスク</div>
    <ul v-for="task in tasks" :key="task.name">
      <li v-if="!task.todo">
        {{ task.name }}
        <button @click="Switch(task.tasknum)">Todo!</button>
      </li>
    </ul>
    <div>完了タスク</div>
    <ul v-for="task in tasks" :key="task.name">
      <li v-if="task.todo">
        {{ task.name }} <button @click="Switch(task.tasknum)">Cansel</button>
      </li>
    </ul>
  </div>
  <div>
    <label>
      新規タスク作成
      <input v-model="newTaskName" type="text" />
    </label>
    <button @click="addTask">追加</button>
  </div>
</template>

<style></style>
