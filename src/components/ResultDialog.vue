<template>
  <div v-if="show" class="dialog">
    <h2>Congratulations!</h2>
    <form @submit.prevent="saveResult">
      <input v-model="username" placeholder="Username" required />
      <input v-model="password" placeholder="Password" type="password" required />
      <button type="submit">Save Result</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  props: {
    show: {
      type: Boolean,
      required: true
    },
    moves: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      username: '',
      password: ''
    };
  },
  methods: {
    saveResult() {
      axios.post('https://localhost:7060/', {
        username: this.username,
        password: this.password,
        score: this.moves
      })
          .then(response => {
            this.$emit('results', response.data);
          });
    }
  }
}
</script>

<style scoped>
.dialog {
  position: fixed;
  background-color: white;
  padding: 20px;
  border-radius: 15px;
  /* Additional styles to center the dialog on the screen */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
