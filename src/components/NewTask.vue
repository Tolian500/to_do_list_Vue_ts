<script setup lang="ts">
import { ref, defineEmits } from 'vue';

// Emits event to the parent component
const emit = defineEmits(['add-task']);

// Reactive state for the new task description
const taskDescription = ref('');

// Add a new task and clear the input field
const addTask = () => {
  if (taskDescription.value.trim()) {
    emit('add-task', { description: taskDescription.value, status: 'Pending' });
    taskDescription.value = ''; // Reset input field
  }
};
</script>

<template>
  <div class="new-task flex items-center gap-2">
    <input
      v-model="taskDescription"
      type="text"
      placeholder="Enter new task"
      class="input border p-2 rounded flex-grow"
    />
    <button @click="addTask" class="button bg-blue-500 text-white px-4 py-2 rounded">
      Add Task
    </button>
  </div>
</template>

<style scoped>
.input {
  flex: 1;
}
.button {
  cursor: pointer;
}
</style>
