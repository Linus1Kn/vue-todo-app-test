<script setup lang="ts">

import { ref } from 'vue';

const emit = defineEmits<{
    addTask: [newTask: string]
}>()

const newTask = ref("")
const error = ref("")

function formSubmitted(){
  if (newTask.value.trim()) {
    emit("addTask", newTask.value.trim())
    newTask.value = ""
    error.value = ""
  } else {
    error.value = "Task cannot be empty"
  }
}

</script>

<template>
    <form @submit.prevent="formSubmitted">
      <label for="">
        New Task
        <input
            @input="error = ''"
            v-model="newTask"
            type="text"
            name="newTask"
            :aria-invalid="!!error || undefined"
        >
        <small v-if="error" id="invalid-helper">
            {{ error }}
        </small>
      </label>

      <div class="button-container">
        <button>Add</button>
      </div>
    </form>
</template>
