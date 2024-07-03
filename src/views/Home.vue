<template>
  <div class="home">
    <h1>Pet Rock Therapy</h1>
    <p>Coins: {{ roundedCoins }}</p>
    <Rock :skin="currentSkin" @increment="incrementCoins" />
    <button @click="openShop">Open Shop</button>
    <Shop :coins="coins" @buy-upgrade="buyUpgrade" @buy-skin="buySkin" ref="shop" />
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
      multiplier: 1,
      autoclickerInterval: null,
      currentSkin: "pet-rock.png",
      currentBaseCoinValue: 1 ,
      purchasedSkins: new Set(),
    };
  },
  computed: {
    roundedCoins() {
      return this.coins.toFixed(1);
    }
  },
  methods: {
    incrementCoins() {
      this.coins += this.currentBaseCoinValue * this.multiplier;
    },
    openShop() {
      this.$refs.shop.openShop();
    },
    buyUpgrade(upgrade) {
      if (this.coins >= upgrade.cost) {
        this.coins -= upgrade.cost;
        if (upgrade.type === "multiplier") {
          this.multiplier += upgrade.multiplier;
        } else if (upgrade.type === "autoclicker") {
          this.activateAutoclicker(upgrade.value);
        } else if (upgrade.type === "music") {
          this.playMusic(upgrade.value);
        }
      }
    },
    buySkin(skin) {
      if (this.coins >= skin.cost && !this.purchasedSkins.has(skin.id)) {
        this.coins -= skin.cost;
        this.currentSkin = skin.image;
        this.currentBaseCoinValue = skin.baseCoinValue;
        this.multiplier = skin.multiplier;
        this.purchasedSkins.add(skin.id);
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
