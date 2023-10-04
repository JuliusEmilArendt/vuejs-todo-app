<script setup>
import TodoCreator from "./CreatorComponent.vue";
import TaskComponent from "./TaskComponent.vue";
import {ref} from 'vue';
import axios from 'axios';
import {base_url} from "@/scripts/constants";
import '../styles/Container.sass';

const taskList = ref([]);
const containerClassName = ref('todo-container');

const createTask = (task) => {
  taskList.value.push(task)
}

const deleteTask = (taskId) => {
  axios.delete(base_url + taskId)
      .then((response) => {
        console.log(response)
      })
      .catch(err => console.log(err));

  taskList.value = taskList.value.filter((task) => {
    return task.id !== taskId
  })
}

const fetchData = async() => {
  try {
    const response = await fetch(base_url)
    taskList.value = await response.json();
  } catch (error) {
    console.log(error)
  }
}

fetchData()
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
            :is-archived="task.isArchived"
        />
      </li>
    </ul>
  </div>
</template>