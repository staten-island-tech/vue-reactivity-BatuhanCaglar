<template>
  <div class="final-display">
    <h2>Final Weapon</h2>
    <img :src="finalWeaponImage" alt="Final Weapon" class="final-weapon-image" />
    <h3>Chosen Weapon: {{ weapon.name }}</h3>
    <h4>Enchantments:</h4>
    <div v-if="enchants.length > 0" class="enchant-list">
      <div v-for="enchant in enchants" :key="enchant" class="chosen-enchant">
        <img :src="getEnchantImage(enchant)" :alt="enchant" class="enchant-image" />
        <span>{{ enchant }}</span>
      </div>
    </div>
    <p v-else>No Enchantments Chosen</p>
    <button @click="$emit('restartGame')" class="restart-button">Restart</button>
  </div>
</template>

<script>
export default {
  props: ['weapon', 'enchants'],
  computed: {
    finalWeaponImage() {
      const weaponMap = { Axe: 'A', Mace: 'M', Scythe: 'Y', Naginata: 'P', Sword: 'S' };
      const enchantMap = { Dark: 'D', Light: 'L', Fire: 'F', Wind: 'W', Lightning: 'T' };
      const weaponLetter = weaponMap[this.weapon.name] || '';
      const folderMap = { Axe: 'axe', Mace: 'mace', Scythe: 'scythe', Naginata: 'spear', Sword: 'sword' };
      const folder = folderMap[this.weapon.name] || '';

      // Show base weapon if no enchantments are selected
      if (this.enchants.length === 0) {
        return `/${folder}/${weaponLetter}.png`;
      }

      // Otherwise, construct the enchanted weapon image filename
      const enchantLetters = this.enchants.map(e => enchantMap[e]).sort().join('');
      return `/${folder}/${weaponLetter}${enchantLetters}.png`;
    }
  },
  methods: {
    getEnchantImage(enchant) {
      const enchantImages = {
        Dark: '/darkball.png',
        Light: '/lightball.png',
        Fire: '/fireballpic.webp',
        Wind: '/windpic.png',
        Lightning: '/lightbolt.png'
      };
      return enchantImages[enchant] || '';
    }
  }
};
</script>


<style>

.final-display {
  text-align: center;
}
.final-weapon-image {
  width: 400px;
  height: auto;
  margin-top: 20px;
}
.enchant-list {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 20px;
}
.chosen-enchant {
  display: flex;
  align-items: center;
  gap: 5px;
}
.enchant-image {
  width: 50px;
  height: 50px;
}
.restart-button {
  background-color: orange;
  padding: 15px;
  border: none;
  cursor: pointer;
  font-size: 1.2rem;
}
h4{
  font-family: "Handjet", sans-serif;
  font-optical-sizing: auto;
  font-size: xx-large;
}

p{
  font-family: "Rajdhani", sans-serif;
  font-weight: 600;
  font-style: normal;
}

</style> 
