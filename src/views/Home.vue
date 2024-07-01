<!-- src/views/Home.vue -->
<template>
  <div class="home">
    <h1>Pet Rock Clicker</h1>
    <p>Coins: {{ coins }}</p>
    <Rock @increment="incrementCoins" />
  </div>
</template>

<script>
import Rock from "@/components/Rock.vue";

export default {
  name: "Home",
  components: {
    Rock
  },
  data() {
    return {
      coins: 0
    };
  },
  methods: {
    incrementCoins() {
      this.coins += 1;
    }
  }
};
</script>

<style scoped>
.home {
  text-align: center;
  margin-top: 50px;
}

h1 {
  font-size: 2em;
}

p {
  font-size: 1.5em;
}
</style>
