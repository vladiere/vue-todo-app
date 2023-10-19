<script setup>
import AllListComponent from '../components/AllListComponent.vue';




</script>

<template>
  <div class="bottom-container">
    <AllListComponent  v-for="index in todoList" :key="index"/>
  </div>
</template>


<style scoped>
.bottom-container {
  margin-top: 1em;
  padding: 10px;
  overflow-y: scroll;
  max-height: calc(100vh - 115px);
}
</style>