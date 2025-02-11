
<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="200" height="80" />

  </header>
  <div class="wrapper">
    <Todo msg="Todo APP" />
  </div>

  <main>
    <TheWelcome />
  </main>
</template>

<script setup lang="ts">
import Todo from './components/Todo.vue'

</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
