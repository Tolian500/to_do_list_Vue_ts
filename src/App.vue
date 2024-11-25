<script setup lang="ts">
import Navbar from '@/components/Navbar.vue'
import Hero from './components/Hero.vue';
import TodoListings from './components/TodoListings.vue'

</script>

<template>
  <Navbar />
  <Hero />
  <TodoListings :limit="3" :showButton="true"/>
</template>