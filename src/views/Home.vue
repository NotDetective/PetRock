<!-- src/views/Home.vue -->
<template>
  <div class="home">
    <h1>Pet Rock Clicker</h1>
    <p>Coins: {{ coins }}</p>
    <Rock @increment="incrementCoins" />
    <button @click="openShop">Open Shop</button>
    <Shop :coins="coins" @buy-upgrade="buyUpgrade" ref="shop" />
  </div>
</template>

<script>
import Rock from "@/components/Rock.vue";
import Shop from "@/components/Shop.vue";

export default {
  name: "Home",
  components: {
    Rock,
    Shop
  },
  data() {
    return {
      coins: 0,
      baseCoinValue: 1,
      multiplier: 1, // Start with a base multiplier of 1
      autoclickerInterval: null,
    };
  },
  methods: {
    incrementCoins() {
      this.coins += this.baseCoinValue * this.multiplier;
    },
    openShop() {
      this.$refs.shop.openShop();
    },
    buyUpgrade(upgrade) {
      if (this.coins >= upgrade.cost) {
        this.coins -= upgrade.cost;
        if (upgrade.type === "multiplier") {
          this.multiplier += upgrade.multiplier; // Correctly add to the multiplier
        } else if (upgrade.type === "autoclicker") {
          this.activateAutoclicker(upgrade.value);
        } else if (upgrade.type === "music") {
          this.playMusic(upgrade.value);
        }
        // Handle more upgrade types here
      }
    },
    activateAutoclicker(clicksPerSecond) {
      if (this.autoclickerInterval) {
        clearInterval(this.autoclickerInterval);
      }
      this.autoclickerInterval = setInterval(() => {
        this.incrementCoins();
      }, 1000 / clicksPerSecond);
    },
    playMusic(file) {
      const audio = new Audio(file);
      audio.loop = true;
      audio.play();
    }
  },
  beforeDestroy() {
    if (this.autoclickerInterval) {
      clearInterval(this.autoclickerInterval);
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

button {
  margin-top: 20px;
  padding: 10px 20px;
  cursor: pointer;
}
</style>
