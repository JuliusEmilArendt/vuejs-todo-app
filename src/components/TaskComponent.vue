<script setup>
import {ref, watch} from 'vue'
import {base_url} from "@/scripts/constants";
import axios from "axios";
import '../styles/TodoTask.sass';

  const props = defineProps({
    id: Number,
    taskDescription: String,
    isDone: Boolean,
    isArchived: Boolean,
    onDelete: Function
  })



  const todoText = ref(props.taskDescription);
  const mark = ref(props.isDone);
  const editing = ref(false);

  const handleEdit = () => {
    const taskObj = {
      taskDescription: todoText.value,
      isDone: mark.value,
      id: props.id,
    }

    axios.put(base_url + props.id, taskObj)
        .then((response) => console.log(response))
        .err(err => console.log(err))
  }

  const toggleEdit = () => {
    editing.value = !editing.value;
  }

  const updateTodoMark = () => {
    const taskObj = {
      taskDescription: todoText.value,
      isDone: mark.value,
      id: props.id
    }

    axios.put(base_url + props.id, taskObj)
        .then(response => console.log(response.data))
        .catch(err => console.log(err))
  }

  watch(mark, updateTodoMark)
</script>

<template>
  <div class="todo">
    <div class="todo-left">
      <div v-if="editing">
        <input type="checkbox" v-model="mark" disabled="disabled" />
        <form @submit="handleEdit" class="edit-form">
          <input type="text" v-model="todoText" class="todo-edit">
        </form>
      </div>
      <div v-else>
        <input type="checkbox" v-model="mark" />
        <span class="todo-text-content">
          {{ todoText }}
        </span>
      </div>



    </div>
    <div class="todo-right">
      <div class="edit-icon" @click="toggleEdit">
        <img
            src="https://www.shareicon.net/data/16x16/2015/09/21/644060_edit_512x512.png"
            alt=""
        />
      </div>
      <div class="delete-icon" @click="props.onDelete(props.id)">
        <img
            src="https://www.shareicon.net/data/32x32/2016/07/09/119083_close_512x512.png"
            alt=""
        />
      </div>
    </div>
  </div>
</template>