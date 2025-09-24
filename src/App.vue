<template>
  <div class="wrapper">
    <h1 class="title">Just simple ToDo app:</h1>
  </div>

  <ToDo />
</template>

<style scoped>
.title {
  text-align: center;
}

</style>

<script setup lang="ts">
import ToDo from "./components/ToDo.vue";
</script>
