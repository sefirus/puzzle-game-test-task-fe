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
}

.empty {
  background-color: #3f1f4b;
  cursor: not-allowed;
  color: transparent;
}
</style>
