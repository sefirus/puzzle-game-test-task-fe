<template>
  <div class="game-board">
    <Cell
        v-for="(cell, index) in cells"
        :key="index"
        :value="cell"
        :index="index"
        @move="moveCell"
    />
  </div>
</template>

<script>
import Cell from "@/components/Cell.vue";

export default {
  name: 'GameBoard',
  components: {Cell},
  data() {
    return {
      cells: this.shuffleCells()
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

      // Check for solvability and correct if necessary
      if (!this.isSolvable(cells)) {
        [cells[14], cells[13]] = [cells[13], cells[14]]; // Swap 2 cells
      }

      return cells;
    },

    isSolvable(cells) {
      let invCount = 0;
      for (let i = 0; i < 16; i++)
        for (let j = i + 1; j < 16; j++)
          if (cells[j] && cells[i] && cells[i] > cells[j])
            invCount++;

      return invCount % 2 === 0;
    },
    moveCell(cellIndex) {
      const emptyIndex = this.cells.indexOf(0);

      // Check if the cell to be moved is next to the empty cell
      const rowDiff = Math.abs(Math.floor(cellIndex / 4) - Math.floor(emptyIndex / 4));
      const colDiff = Math.abs(cellIndex % 4 - emptyIndex % 4);

      if ((rowDiff === 1 && colDiff === 0) || (rowDiff === 0 && colDiff === 1)) {
        this.cells[emptyIndex] = this.cells[cellIndex];
        this.cells[cellIndex] = 0;
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

.cell {
  width: 60px;
  height: 60px;
  line-height: 60px;
  text-align: center;
  background-color: #ffeb95;
  color: #3f1f4b;
}
</style>
