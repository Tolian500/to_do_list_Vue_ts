<script setup>
import { defineProps } from 'vue';

defineProps({
  todo: Object,
})

</script>

<template>
  <div class="bg-white rounded-xl shadow-md relative">
    <div class="p-4">
      <div class="mb-6">
        <div class="text-gray-600 my-2">{{ todo.id }}</div>
        <h3 class="text-xl font-bold">{{ todo.title }}</h3>
      </div>

      <div class="mb-5">
        <div v-for="(task, index) in todo.tasks" :key="index" class="task-item flex items-center mb-2">
          <!-- Checkbox -->
          <input type="checkbox" v-model="task.completed" class="mr-2" />

          <!-- Task Text -->
          <span class="flex-1" :class="{ 'line-through': task.completed }">
            {{ index + 1 }}. {{ task.description }}
          </span>

          <!-- Pen Icon -->
          <button class="ml-2 text-blue-500 hover:text-blue-700" @click="editTask(task)">
            ✏️
          </button>
        </div>
      </div>
      <div class="border border-gray-100 mb-5"></div>

      <div class="flex flex-col lg:flex-row justify-between mb-4">
        <a href="job.html"
          class="h-[36px] bg-blue-200 hover:bg-blue-300 text-back px-4 py-2 rounded-lg text-center text-sm">
          Copy list
        </a>
      </div>
      <div class="flex flex-col lg:flex-row justify-between mb-4">
        <a href="job.html"
          class="h-[36px] bg-yellow-500 hover:bg-yellow-600 text-black px-4 py-2 rounded-lg text-center text-sm">
          Mark All Done
        </a>
      </div>
    </div>
  </div>

</template>