<template>
  <div class="weapon-selection">
    <h2>Select Your Weapon</h2>
    <div class="weapon-carousel">
      <button @click="prevWeapon" class="carousel-btn">◀</button>
      <img :src="weapons[currentIndex].image" :alt="weapons[currentIndex].name" class="weapon-image" />
      <button @click="nextWeapon" class="carousel-btn">▶</button>
    </div>
    <button @click="selectWeapon" class="select-button">Next</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentIndex: 0,
      weapons: [
        { name: 'Axe', image: '/AXE.png' },
        { name: 'Mace', image: '/MACE.png' },
        { name: 'Naginata', image: '/NAGINATA.png' },
        { name: 'Scythe', image: '/SCYTHE.png' },
        { name: 'Sword', image: '/SWORD.png' }
      ]
    };
  },
  methods: {
    prevWeapon() {
      this.currentIndex = (this.currentIndex - 1 + this.weapons.length) % this.weapons.length;
    },
    nextWeapon() {
      this.currentIndex = (this.currentIndex + 1) % this.weapons.length;
    },
    selectWeapon() {
      this.$emit('selectWeapon', this.weapons[this.currentIndex]);
    }
  }
};
</script>

<style>

h2{
  font-family: "Handjet", sans-serif;
  font-optical-sizing: auto;
  font-size: xx-large;
}

.weapon-selection {
  text-align: center;
  font-family: "Rajdhani", sans-serif;
  font-weight: 300;
  font-style: normal;
}
.weapon-carousel {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
}
.weapon-image {
  width: 35rem;
  height: auto;
  border-radius: 50%;
  transition: transform 0.3s ease-in-out;
}
.carousel-btn {
  background-color: orange;
  border: none;
  padding: 10px;
  cursor: pointer;
  font-size: 1.5rem;
}
.select-button {
  margin-top: 20px;
  background-color: orange;
  padding: 15px;
  border: none;
  cursor: pointer;
  font-size: 1.2rem;
  font-family: "Rajdhani", sans-serif;
  font-weight: 300;
  font-style: normal;
}
</style>
