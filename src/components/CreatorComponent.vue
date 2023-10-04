<script setup>
  import { ref } from "vue";

  const props = defineProps({
    onSubmit: Function
  })

  const creatorClassName = ref("todo-creator")
  const taskDescription = ref("")
  const inputClassName = ref("todo-input")

  function handleSubmit(e) {
    e.preventDefault()
    props.onSubmit(taskDescription.value)
    taskDescription.value = ""
  }
</script>

<template>
  <div :class="creatorClassName">
    <form :class="creatorClassName" @submit="handleSubmit">
      <input
        type="text"
        placeholder="Add some todo..."
        v-model="taskDescription"
        :class="inputClassName"
      />
    </form>
  </div>
</template>

<style scoped>

</style>