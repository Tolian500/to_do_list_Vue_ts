<script setup>
import TodoListing from './TodoListing.vue';
import todoData from '@/todos.json'
import { ref, defineProps } from 'vue';

defineProps({
    limit: Number,
    showButton: {
        type: Boolean,
        default: false
    }

})

const todos = ref(todoData)
console.log(todos.value)

</script>

<template>
    <section class="bg-yellow-50 px-4 py-10">
        <div class="container-xl lg:container m-auto">
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">

            <TodoListing v-for="todo in todos.slice(0,limit || todos.lenght)" :key="todo.id" :todo="todo"/>
        </div>
    </section>
    <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
      <a
        href="/todos"
        class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
        >View All Jobs</a
      >
    </section>
</template>