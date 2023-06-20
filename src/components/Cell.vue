<template>
  <div
      class="cell"
      :class="{ empty: value === 0 }"
      @click="moveCell"
  >
    {{ value === 0 ? '' : value }}
  </div>
</template>

<script>
export default {
  name: 'Cell',
  props: {
    value: {
      type: Number,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  methods: {
    moveCell() {
      this.$emit('move', this.index);
    }
  }
}
</script>

<style scoped>
.cell {
  width: 60px;
  height: 60px;
  line-height: 60px;
  text-align: center;
  background-color: #ffeb95;
  color: #3f1f4b;
  border-radius: 15px; /* Add rounded corners */
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.2); /* Add box-shadow for 3D effect */
  transition: all 0.1s ease-in-out; /* Add transition for smooth movement */
}

.empty {
  background-color: #3f1f4b;
  cursor: not-allowed;
  color: transparent;
  box-shadow: none; /* Remove box-shadow from the empty cell */
}
</style>
