<template>
  <div class="user-results">
    <h2>Your Results</h2>
    <div v-for="result in results" :key="result.timestamp" class="result">
      <p>Moves: {{ result.movesCount }}</p>
      <p>Time: {{ formatDate(result.timestamp) }}</p>
    </div>
  </div>
</template>

<script>
// ...

import axios from "axios";

export default {
  // ...
  props: {
    results: []
  },
  methods: {
    formatDate(timestamp) {
      const date = new Date(timestamp);
      return `${date.getDate()}-${date.getMonth()+1}-${date.getFullYear()} ${date.getHours()}:${date.getMinutes()}`;
    },
  }
  // ...
}
</script>

<style scoped>
.user-results {
  margin: 20px;
  width: 200px;
}

.result {
  background-color: #ffeb95;
  color: #3f1f4b;
  border-radius: 15px;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.2);
  margin: 10px 0;
  padding: 10px;
}
</style>
