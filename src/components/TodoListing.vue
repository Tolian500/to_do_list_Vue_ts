<script setup>
import { defineProps, ref, computed } from 'vue';

// Props
const props = defineProps({
  todo: Object,
});

// Reactive state
const showFullTasks = ref(false);

// Computed property for truncated tasks
const truncatedTasks = computed(() => {
  const tasks = props.todo.tasks;
  if (!showFullTasks.value && tasks.length > 4) {
    return tasks.slice(0, 4); // Show only the first 4 tasks
  }
  return tasks; // Show all tasks
});

// Methods
const editTask = (task) => {
  const newText = prompt("Edit task:", task.description);
  if (newText !== null) {
    task.description = newText;
  }
};

const deleteTask = (taskIndex) => {
  props.todo.tasks.splice(taskIndex, 1);
};

const addNewTask = () => {
  const newTaskDescription = prompt("Enter the new task description:");
  if (newTaskDescription) {
    props.todo.tasks.push({
      id: `${props.todo.id}.${props.todo.tasks.length + 1}`,
      description: newTaskDescription,
      status: "Pending",
    });
  }
};
</script>

<template>
  <div class="bg-white rounded-xl shadow-md relative flex flex-col">
    <div class="p-4 flex-grow">
      <div class="mb-6">
        <div class="text-gray-600 my-2">List ID: {{ todo.id }}</div>
        <h3 class="text-xl font-bold">{{ todo.title }}</h3>
      </div>

      <div class="mb-2">
        <div
          v-for="(task, index) in truncatedTasks"
          :key="task.id"
          class="task-item flex items-center mb-2"
        >
          <!-- Checkbox -->
          <input type="checkbox" v-model="task.status" class="mr-2" />

          <!-- Task Text -->
          <span class="flex-1" :class="{ 'line-through': task.status === 'Completed' }">
            {{ index + 1 }}. {{ task.description }}
          </span>

          <!-- Pen Icon -->
          <button
            class="ml-2 text-blue-500 hover:text-blue-700"
            @click="editTask(task)"
          >
            ✏️
          </button>

          <!-- Trash Icon -->
          <button
            class="ml-2 text-red-500 hover:text-red-700"
            @click="deleteTask(index)"
          >
            🗑️
          </button>
        </div>

        <!-- Add New Task Line -->
        <div
          class="flex items-center text-blue-500 cursor-pointer hover:underline mt-2"
          @click="addNewTask"
        >
          + Add new task
        </div>
      </div>

      <!-- Show More/Show Less Toggle -->
      <div
        v-if="todo.tasks.length > 4"
        class="text-sm text-blue-500 cursor-pointer hover:underline mt-4"
        @click="showFullTasks = !showFullTasks"
      >
        {{ showFullTasks ? "Show less" : "Show more" }}
      </div>
    </div>

    <!-- Divider -->
    <div class="border border-gray-100 mb-2"></div>

    <!-- Buttons anchored to the bottom -->
    <div class="p-4 mt-auto">
      <div class="flex flex-col lg:flex-row justify-between gap-4">
        <a
          href="job.html"
          class="h-[36px] bg-blue-200 hover:bg-blue-300 text-back px-4 py-2 rounded-lg text-center text-sm"
        >
          Copy list
        </a>
        <a
          href="job.html"
          class="h-[36px] bg-yellow-500 hover:bg-yellow-600 text-black px-4 py-2 rounded-lg text-center text-sm"
        >
          Mark All Done
        </a>
      </div>
    </div>
  </div>
</template>
