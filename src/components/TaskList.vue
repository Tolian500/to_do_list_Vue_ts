<script setup lang="ts">
import { ref } from 'vue';
import NewTask from './NewTask.vue';
import TaskItem from './TaskItem.vue';

// Define the Task type
type Task = {
  id: string;
  description: string;
  status: "Pending" | "Completed";  
};

// Import the todos.json file
import todosData from '@/todos.json'; // Assuming todos.json is located in the 'src' folder

// Define reactive tasks list from the imported JSON
const tasks = ref(todosData); // Initialize tasks with data from the JSON

// Add a new task
const addTask = (task: { description: string; status: "Pending" | "Completed"; }) => {
  const newTask: Task = {
    id: `${tasks.value[0].tasks.length + 1}`,  // Ensuring each task has a unique id
    description: task.description,
    status: task.status,  // Ensure status is either "Pending" or "Completed"
  };
  
  // Add new task at the top of the first list (you can modify the list as needed)
  tasks.value[0].tasks.unshift(newTask);
};

// Delete a task by index
const deleteTask = (todoId: string, taskIndex: number) => {
  const todo = tasks.value.find(t => t.id === todoId);
  if (todo) {
    todo.tasks.splice(taskIndex, 1);
  }
};

// Update a task (e.g., toggle status, edit description)
const updateTask = (todoId: string, updatedTask: Task) => {
  const todo = tasks.value.find(t => t.id === todoId);
  if (todo) {
    const taskIndex = todo.tasks.findIndex((t) => t.id === updatedTask.id);
    if (taskIndex !== -1) {
      todo.tasks[taskIndex] = updatedTask;
    }
  }
};
</script>

<template>
  <div class="task-list bg-white p-4 rounded shadow">
    <!-- New task input -->
    <NewTask @add-task="addTask" />

    <!-- Task items -->
    <div class="tasks mt-4">
      <div
        v-for="todo in tasks"
        :key="todo.id"
        class="todo-list"
      >
        <div v-for="(task, index) in todo.tasks" :key="task.id">
          <TaskItem
            :task="task"
            :index="index"
            @delete-task="deleteTask(todo.id, index)"
            @update-task="updateTask(todo.id, task)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.task-list {
  max-width: 600px;
  margin: 0 auto;
}
</style>
