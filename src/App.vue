<script setup>
import { RouterLink, RouterView } from 'vue-router';
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo_large.svg" height="125" />

    <div class="wrapper">

    </div>
  </header>
  <nav>
    <ul>
      <li>
        <RouterLink to="/">Accueil</RouterLink>
      </li>
      <li>
        <RouterLink to="/about">À propos</RouterLink>
      </li>
    </ul>
  </nav>
  <RouterView />
  <footer>&copy; 2023</footer>
</template>

