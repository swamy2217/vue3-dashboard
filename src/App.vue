<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">Home2</RouterLink>
        <RouterLink to="/datatables">Data tables</RouterLink>
      </nav>
  </header>
  <div class="container">
    <RouterView />
  </div>

</template>

<style scoped>
.container {
  margin: 0 20px;
}
header {
  margin: 3px 40px;
  a {
    margin-right: 1rem;
  }
}
</style>
