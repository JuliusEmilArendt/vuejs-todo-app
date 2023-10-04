<script setup>
import TodoCreator from "./CreatorComponent.vue"
import TaskComponent from "./TaskComponent.vue"
// eslint-disable-next-line no-unused-vars
import { ref } from 'vue';

let id = 0;

const taskList = ref([
  {
    id: id++,
    taskDescription: "some kind of text",
    deadLine: "23.04.2023",
    isDone: false,
    isArchived: false
  },
  {
    id: id++,
    taskDescription: "anotherTask",
    deadLine: "23.04.2023",
    isDone: false,
    isArchived: false
  },
  {
    id: id++,
    taskDescription: "anotherTask",
    deadLine: "23.04.2023",
    isDone: false,
    isArchived: false
  }
])
const containerClassName = ref('todo-container')

const createTask = (taskDescription) => {
  taskList.value.push(
      {
        id: id++,
        taskDescription: taskDescription,
        deadLine: "23.04.2023",
        isDone: false,
        isArchived: false
      }
  )
}

const deleteTask = (taskId) => {
  taskList.value = taskList.value.filter((task) => {
    return task.id !== taskId
  })
}

</script>

<template>
  <div :class=containerClassName>
    <h1>What&apos;s the plan for Today?</h1>
    <TodoCreator :on-submit="createTask" />
    <ul>
      <li v-for="task in taskList" :key="task.id">
        <TaskComponent
            :id="task.id"
            :is-done="task.isDone"
            :task-description="task.taskDescription"
            :on-delete="deleteTask"
        />
      </li>
    </ul>
  </div>
</template>

<style scoped>

</style>