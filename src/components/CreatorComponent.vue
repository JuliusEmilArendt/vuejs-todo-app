<script setup>
  import { ref } from "vue";
  import axios from "axios";
  import {base_url} from "@/scripts/constants";
  import '../styles/TodoCreator.sass';

  const props = defineProps({
    onSubmit: Function
  })

  const creatorClassName = ref("todo-creator")
  const taskDescription = ref("")
  const inputClassName = ref("todo-input")

  function handleSubmit() {
    const taskObject = {
      isDone: false,
      isArchived: false,
      taskDescription: taskDescription.value
    }
    axios.post(base_url, taskObject)
        .then((response) => {
          props.onSubmit(response.data)
        })
        .catch(err => console.log(err))
    taskDescription.value = ""
  }
</script>

<template>
  <div :class="creatorClassName">
    <form :class="creatorClassName" @submit.prevent="handleSubmit">
      <input
        type="text"
        placeholder="Add some todo..."
        v-model="taskDescription"
        :class="inputClassName"
      />
    </form>
  </div>
</template>