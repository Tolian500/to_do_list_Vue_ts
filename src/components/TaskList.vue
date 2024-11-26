<script setup lang="ts">
import { ref } from 'vue';
import NewTask from './NewTask.vue';
import TaskItem from './TaskItem.vue';

// Define reactive tasks list
const tasks = ref([
  { id: '1', description: 'Sample Task 1', status: 'Pending' },
  { id: '2', description: 'Sample Task 2', status: 'Completed' },
]);

// Add a new task
const addTask = (task: { description: string; status: string }) => {
  const newTask = { id: `${tasks.value.length + 1}`, ...task };
  tasks.value.push(newTask);
};

// Delete a task by index
const deleteTask = (index: number) => {
  tasks.value.splice(index, 1);
};

// Update a task (e.g., toggle status, edit description)
const updateTask = (updatedTask: { id: string; description: string; status: string }) => {
  const taskIndex = tasks.value.findIndex((t) => t.id === updatedTask.id);
  if (taskIndex !== -1) {
    tasks.value[taskIndex] = updatedTask;
  }
};
</script>

<template>
  <div class="task-list bg-white p-4 rounded shadow">
    <!-- New task input -->
    <NewTask @add-task="addTask" />

    <!-- Task items -->
    <div class="tasks mt-4">
      <TaskItem
        v-for="(task, index) in tasks"
        :key="task.id"
        :task="task"
        :index="index"
        @delete-task="deleteTask"
        @update-task="updateTask"
      />
    </div>
  </div>
</template>

<style scoped>
.task-list {
  max-width: 600px;
  margin: 0 auto;
}
</style>
