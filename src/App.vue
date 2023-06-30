<script setup>
import { RouterView } from 'vue-router';
import NavComponent from '@/components/Nav.vue';
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo_large.svg" height="125" />
  <NavComponent />
  </header>
  <RouterView />
  <footer>&copy; 2023</footer>
</template>

