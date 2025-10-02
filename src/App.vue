<script setup>
import { ref, onMounted } from 'vue';

  const message = ref('Hello world!');
  const status = ref('active');
  const tasks = ref(['one', 'two', 'three', 'four']);
  const newTask = ref('');

  const toggleStatus = () => {
    if (status.value === 'active') {
      status.value = 'pending';
    } else if (status.value === 'pending') {
      status.value = 'inactive';
    } else {
      status.value = 'active';
    }
  };

  const addTask = () => {
    if (newTask.value !== '') {
      tasks.value.push(newTask.value);
      newTask.value = '';
    }
  };

  const deleteTask = (index) => {
    tasks.value.splice(index, 1);
  };

  onMounted(async () => {
    try {
      const response = await fetch('http://jsonplaceholder.typicode.com/todos');
      const data = await response.json();
      tasks.value = data.slice(9, 20).map((task) => task.title);
    } catch (error) {
      console.log(error);
    }
  });
</script>

<template>
  <h1>{{ message }}</h1>
  <p>user is {{ status }}</p>

  <form @submit.prevent='addTask'>
    <label for='newTask'>Add Task</label>
    <input type='text' id='newTask' name='newTask' v-model='newTask' />
    <button type='submit'>Submit</button>
  </form>

  <h3>Tasks: </h3>
  <ul>
    <li v-for='(task, index) in tasks' :key='task'>
      <span>
        {{ task }}
      </span>
      <button @click='deleteTask(index)'>x</button>
    </li>
  </ul>

  <button @click='toggleStatus'>Change status</button>
</template>