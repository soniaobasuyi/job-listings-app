<script setup>
import { ref } from 'vue';

  const message = ref("Hello world!");
  const status = ref("active");
  const tasks = ref(["one", "two", "three", "four"]);

  const toggleStatus = () => {
    if (status.value === "active") {
      status.value = "pending";
    } else if (status.value === "pending") {
      status.value = "inactive";
    } else {
      status.value = "active";
    }
  };
</script>

<template>
  <h1>{{ message }}</h1>
  <p>user is {{ status }}</p>

  <h3>Tasks: </h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>

  <button @click="toggleStatus">Change status</button>
</template>