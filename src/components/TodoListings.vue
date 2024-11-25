<script setup>
import TodoListing from './TodoListing.vue';
import todoData from '@/todos.json'
import { ref } from 'vue';

const todos = ref(todoData)
console.log(todos.value)

</script>

<template>
    <section class="bg-yellow-50 px-4 py-10">
        <div class="container-xl lg:container m-auto">
            <h2 class="text-3xl font-bold text-yellow-700 mb-6 text-center">
                List
            </h2>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">

            <TodoListing v-for="todo in todos" :key="todo.id" :todo="todo"/>
        </div>
    </section>
</template>