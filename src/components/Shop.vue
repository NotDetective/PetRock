<template>
  <div class="shop" v-if="visible">
    <div class="shop-content">
      <h2>Shop</h2>
      <div class="shop-sections">
        <div class="upgrades-section">
          <h3>Upgrades</h3>
          <ul>
            <li v-for="upgrade in upgrades" :key="upgrade.id">
              <div class="upgrade">
                <span>{{ upgrade.name }}</span>
                <span>{{ upgrade.cost }} coins</span>
                <button @click="buyUpgrade(upgrade)" :disabled="coins < upgrade.cost">Buy</button>
              </div>
            </li>
          </ul>
        </div>
        <div class="skins-section">
          <h3>Skins</h3>
          <ul>
            <li v-for="skin in skins" :key="skin.id">
              <div class="skin">
                <img :src="`${skin.image}`" :alt="skin.name" class="skin-image"/>
                <span>{{ skin.name }}</span>
                <span>{{ skin.cost }} coins</span>
                <button @click="buySkin(skin)" :disabled="coins < skin.cost || purchasedSkins.has(skin.id)">Buy</button>
              </div>
            </li>
          </ul>
        </div>
      </div>
      <button class="close" @click="closeShop">Close</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Shop",
  props: {
    coins: Number,
    purchasedSkins: {
      type: Set,
      default: () => new Set(),
    }
  },
  data() {
    return {
      visible: false,
      upgrades: [
        { id: 1, name: "+1 Multiplier", cost: 100, type: "multiplier", multiplier: 1 },
        { id: 2, name: "+2 Multiplier", cost: 300, type: "multiplier", multiplier: 2 },
        { id: 3, name: "Autoclicker", cost: 5000, type: "autoclicker", value: 1 },
      ],
      skins: [
        {id: 1, name: "Rock-OwO", cost: 1000, image: "Rock-OwO.png", type: "skin", baseCoinValue: 0.12, multiplier: 10},
        {
          id: 2,
          name: "Rock-Gamba",
          cost: 1500,
          image: "Rock-Gamba.png",
          type: "skin",
          baseCoinValue: 0.14,
          multiplier: 12
        },
        {
          id: 3,
          name: "Rock-Toga",
          cost: 2000,
          image: "Rock-Toga.png",
          type: "skin",
          baseCoinValue: 0.18,
          multiplier: 14
        },
        {
          id: 4,
          name: "Rock-Miku",
          cost: 2500,
          image: "Rock-Miku.png",
          type: "skin",
          baseCoinValue:0.20,
          multiplier: 16
        },
        {
          id: 5,
          name: "Rock",
          cost: 3000,
          image: "Rock-Neko-1.png",
          type: "skin",
          baseCoinValue: 0.22,
          multiplier: 18
        },
        {
          id: 6,
          name: "Rock",
          cost: 3500,
          image: "Rock-Neko-2.png",
          type: "skin",
          baseCoinValue: 0.24,
          multiplier: 20
        },
        {
          id: 7,
          name: "Rock-Kafka",
          cost: 4000,
          image: "Rock-Kafka.png",
          type: "skin",
          baseCoinValue: 0.30,
          multiplier: 20
        },
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
    },
    buySkin(skin) {
      this.$emit('buy-skin', skin);
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

.shop-sections {
  display: flex;
  justify-content: space-between;
}

.upgrades-section, .skins-section {
  width: 45%;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin: 10px 0;
}

.upgrade, .skin {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.skin-image {
  width: 50px;
  height: 50px;
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
