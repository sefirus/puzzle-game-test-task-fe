<template>
  <div>
    <p>Moves: {{ moves }}</p>
    <div class="game-board">
      <Cell
          v-for="(cell, index) in cells"
          :key="index"
          :value="cell"
          :index="index"
          @move="moveCell"
      />
    </div>
  </div>
</template>

<script>
import Cell from "@/components/Cell.vue";

export default {
  name: 'GameBoard',
  components: {Cell},
  data() {
    return {
      cells: this.shuffleCells(),
      moves: 0 // added
    };
  },
  methods: {
    shuffleCells() {
      let cells = Array.from({length: 15}, (_, i) => i + 1);
      cells.push(0);  // The empty cell

      // Shuffle the cells
      for(let i = cells.length - 1; i > 0; i--){
        const j = Math.floor(Math.random() * (i + 1));
        [cells[i], cells[j]] = [cells[j], cells[i]];
      }

      return cells;
    },

    moveCell(cellIndex) {
      const emptyIndex = this.cells.indexOf(0);

      // Check if the cell to be moved is next to the empty cell
      const rowDiff = Math.abs(Math.floor(cellIndex / 4) - Math.floor(emptyIndex / 4));
      const colDiff = Math.abs(cellIndex % 4 - emptyIndex % 4);

      if ((rowDiff === 1 && colDiff === 0) || (rowDiff === 0 && colDiff === 1)) {
        this.cells[emptyIndex] = this.cells[cellIndex];
        this.cells[cellIndex] = 0;
        this.moves++; // added
      }

      if (this.isSolved()) {
        alert("Congratulations! You solved the puzzle!");
      }
    },
    isSolved() {
      for (let i = 0; i < 15; i++) {
        if (this.cells[i] !== i + 1) {
          return false;
        }
      }
      return this.cells[15] === 0;
    }
  }
}
</script>

<style scoped>
.game-board {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}
</style>
