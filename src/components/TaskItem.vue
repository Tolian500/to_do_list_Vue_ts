<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';

// Props and emits
const props = defineProps({
  task: {
    type: Object as () => { id: string; description: string; status: 'Pending' | 'Completed' },
    required: true,
  },
  index: Number,
});

const emit = defineEmits(['delete-task', 'update-task']);

// Toggle task completion status
const toggleStatus = () => {
  props.task.status = props.task.status === 'Completed' ? 'Pending' : 'Completed';
  emit('update-task', props.task);
};

// Edit task description
const editTask = () => {
  const newText = prompt('Edit task:', props.task.description);
  if (newText !== null) {
    props.task.description = newText;
    emit('update-task', props.task);
  }
};

// Delete task
const deleteTask = () => {
  emit('delete-task', props.index);
};
</script>

<template>
  <div class="task-item flex items-center gap-2 p-2 border-b">
    <!-- Task status checkbox -->
    <input
      type="checkbox"
      :checked="task.status === 'Completed'"
      @change="toggleStatus"
      class="mr-2"
    />

    <!-- Task description -->
    <span :class="{ 'line-through text-gray-500': task.status === 'Completed' }">
      {{ task.description }}
    </span>

    <!-- Edit button -->
    <button @click="editTask" class="text-blue-500 hover:text-blue-700 ml-2">
      ✏️
    </button>

    <!-- Delete button -->
    <button @click="deleteTask" class="text-red-500 hover:text-red-700 ml-2">
      🗑️
    </button>
  </div>
</template>

<style scoped>
.line-through {
  text-decoration: line-through;
}
</style>
