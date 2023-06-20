<template>
  <div class="app-container">
    <GameBoard @results="handleResults" @game-over="gameOver = $event" />
    <UserResults :results="userResults" />
    <Leaderboard ref="leaderboard" />
    <ResultDialog v-if="gameOver" :moves="moves" @results="handleResults" @close="gameOver = false"  show/>
  </div>
</template>

<script>
import GameBoard from './components/GameBoard.vue'
import Leaderboard from "@/components/Leaderboard.vue";
import UserResults from "@/components/UserResults.vue";
import userResults from "@/components/UserResults.vue";

export default {
  name: 'App',
  computed: {
    userResults() {
      return userResults
    }
  },
  props: {
    gameOver: false
  },
  components: {
    UserResults,
    Leaderboard,
    GameBoard
  },
  methods: {
    handleResults(results) {
      this.userResults = results;
      this.$refs.leaderboard.fetchData();
      this.gameOver = false;
    },
  }
}
</script>

<style>
.app-container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
}
</style>
