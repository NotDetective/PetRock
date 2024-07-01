<!-- src/components/Rock.vue -->
<template>
  <div class="rock-container">
    <img src="@/assets/pet-rock.png" alt="Pet Rock" @click="incrementCoins" class="rock" />
  </div>
</template>

<script>
export default {
  name: "Rock",
  methods: {
    incrementCoins() {
      this.$emit('increment');
    }
  }
};
</script>

<style scoped>
.rock-container {
  text-align: center;
  margin-top: 20px;
}

.rock {
  width: 200px;
  height: auto;
  cursor: pointer;
}
</style>
