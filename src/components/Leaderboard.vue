<template>
  <div class="leaderboard">
    <h2>Leaderboard</h2>
    <div v-for="(entry, index) in leaderboard" :key="entry.timestamp" :class="['card', { 'highlight': index === 0 }]">
      <p>{{ entry.username }}</p>
      <p>Moves: {{ entry.movesCount }}</p>
      <p>Time: {{ formatDate(entry.timestamp) }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Leaderboard',
  data() {
    return {
      leaderboard: [],
    };
  },
  methods: {
    fetchData() {
      axios.get('https://localhost:7060/leaderboard')
          .then(response => {
            this.leaderboard = response.data;
          });
    },
    formatDate(timestamp) {
      const date = new Date(timestamp);
      return `${date.getDate()}-${date.getMonth()+1}-${date.getFullYear()} ${date.getHours()}:${date.getMinutes()}`;
    },
  },
  mounted() {
    this.fetchData();
  }
}
</script>

<style scoped>
.leaderboard {
  margin: 20px;
}

.card {
  background-color: #ffeb95;
  color: #3f1f4b;
  border-radius: 15px;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.2);
  margin: 10px 0;
  padding: 10px;
}

.highlight {
  background-color: #ffd700;
}
</style>
