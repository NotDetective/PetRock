<template>
  <div class="rock-container">
    <img :src="rockImageSrc" alt="Pet Rock" @click="incrementCoins" class="rock" @error="imageError" />
  </div>
</template>

<script>
export default {
  name: "Rock",
  props: {
    skin: {
      type: String,
      required: true,
      default: "pet-rock.png"
    }
  },
  data() {
    return {
      rockImageSrc: ''
    }
  },
  watch: {
    skin: {
      immediate: true,
      handler(newSkin) {
        this.updateRockImageSrc(newSkin);
      }
    }
  },
  methods: {
    incrementCoins() {
      this.$emit('increment');
    },
    imageError() {
      console.error(`Image not found: ${this.rockImageSrc}`);
      this.rockImageSrc = 'pet-rock.png'; // Fallback image
    },
    updateRockImageSrc(skin) {
      this.rockImageSrc = skin;
    }
  },
  mounted() {
    this.updateRockImageSrc(this.skin);
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
