<script>
export default {
  data() {
    return {
      welcome: "Hello World!",
      status: "active",
      tasks: ["one", "two", "three", "four", "five"],
      link: "https://google.com",
    };
  },
  methods: {
    toggleStatus () {
      if (this.status === "active") {
        this.status = "pending";
      } else if (this.status === "pending") {
        this.status = "inactive";
      } else {
        this.status = "active";
      }
    }
  },
};
</script>

<template>
  <h1>{{ welcome }}</h1>
  <h3>Tasks: </h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>

<!--  <a v-bind:href="link" target="_blank">open google</a> or alternatively; -->
  <a :href="link" target="_blank">open google</a>

  <p>user is {{ status }}</p>

<!--  <button v-on:click="toggleStatus">Change status</button> or alternatively;  -->
  <button @click="toggleStatus">Change status</button>
</template>