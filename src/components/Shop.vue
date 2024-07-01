<!-- src/components/Shop.vue -->
<template>
  <div class="shop" v-if="visible">
    <div class="shop-content">
      <h2>Shop</h2>
      <ul>
        <li v-for="upgrade in upgrades" :key="upgrade.id">
          <div class="upgrade">
            <span>{{ upgrade.name }}</span>
            <span>{{ upgrade.cost }} coins</span>
            <button @click="buyUpgrade(upgrade)" :disabled="coins < upgrade.cost">Buy</button>
          </div>
        </li>
      </ul>
      <button class="close" @click="closeShop">Close</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Shop",
  props: {
    coins: Number
  },
  data() {
    return {
      visible: false,
      upgrades: [
        { id: 1, name: "+1 Multiplier", cost: 100, type: "multiplier", multiplier: 1 },
        { id: 2, name: "+2 Multiplier", cost: 300, type: "multiplier", multiplier: 2 },
        { id: 3, name: "Autoclicker", cost: 500, type: "autoclicker", value: 1 },
        { id: 4, name: "Background Music", cost: 200, type: "music", value: "background.mp3" },
        // Add more functional upgrades here
      ]
    };
  },
  methods: {
    openShop() {
      this.visible = true;
    },
    closeShop() {
      this.visible = false;
    },
    buyUpgrade(upgrade) {
      this.$emit('buy-upgrade', upgrade);
    }
  }
};
</script>

<style scoped>
.shop {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.shop-content {
  background: white;
  padding: 20px;
  border-radius: 10px;
  text-align: center;
}

.upgrade {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 10px 0;
}

button {
  padding: 5px 10px;
  cursor: pointer;
}

button:disabled {
  cursor: not-allowed;
  opacity: 0.5;
}

.close {
  margin-top: 20px;
}
</style>
