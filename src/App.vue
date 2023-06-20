<template>
  <div id="app">
    <GameBoard/>
    <Leaderboard/>
  </div>
</template>

<script>
import GameBoard from './components/GameBoard.vue'
import Leaderboard from "@/components/Leaderboard.vue";

export default {
  name: 'App',
  components: {
    Leaderboard,
    GameBoard
  },
}
</script>
