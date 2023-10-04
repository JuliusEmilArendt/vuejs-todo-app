<script setup>
  const props = defineProps({
    id: Number,
    taskDescription: String,
    isDone: Boolean,
    onDelete: Function
  })
</script>

<template>
  {{props.taskDescription}}
  <button @click="onDelete(props.id)">X</button>
</template>

<style scoped>

</style>