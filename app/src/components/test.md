<template>
  <div>
    <div v-if="!selectedWeapon" class="carousel w-full">
      <div
        v-for="(weapon, index) in weapons"
        :key="weapon.name"
        :id="`item${index + 1}`"
        class="carousel-item w-full"
      >
        <img
          :src="weapon.image"
          :alt="weapon.name"
          class="w-full cursor-pointer"
          @click="selectWeapon(weapon)"
        />
      </div>
    </div>

    <div v-if="!selectedWeapon" class="flex w-full justify-center gap-2 py-2">
      <a
        v-for="(weapon, index) in weapons"
        :key="weapon.name"
        :href="`#item${index + 1}`"
        class="btn btn-xs"
      >
        {{ index + 1 }}
      </a>
    </div>

    <div v-if="selectedWeapon" class="selected-weapon">
      <img :src="getWeaponImage()" :alt="selectedWeapon.name" class="w-full" />
      <h2 class="text-center text-xl font-bold">{{ selectedWeapon.name }}</h2>
      
      <div class="enchantments">
        <button v-for="enchantment in enchantments" :key="enchantment" @click="toggleEnchantment(enchantment)" :class="{'selected': selectedEnchantments.includes(enchantment)}" class="btn enchantment-btn">
          {{ enchantment }}
        </button>
      </div>
      
      <button @click="resetSelection" class="btn mt-4">Restart</button>
      <button v-if="selectedEnchantments.length" @click="confirmSelection" class="btn mt-4">Confirm</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const weapons = [
  { name: 'Greataxe', prefix: 'A', image: '/AXE.png' },
  { name: 'Longsword', prefix: 'S', image: '/SWORD.png' },
  { name: 'Scythe', prefix: 'Y', image: '/SCYTHE.png' },
  { name: 'Mace', prefix: 'M', image: '/MACE.png' },
  { name: 'Naginata', prefix: 'P', image: '/NAGINATA.png' },
]

const enchantments = ['Dark', 'Light', 'Fire', 'Wind', 'Lightning']
const selectedWeapon = ref(null)
const selectedEnchantments = ref([])

const selectWeapon = (weapon) => {
  selectedWeapon.value = weapon
  selectedEnchantments.value = []
}

const toggleEnchantment = (enchantment) => {
  if (selectedEnchantments.value.includes(enchantment)) {
    selectedEnchantments.value = selectedEnchantments.value.filter(e => e !== enchantment)
  } else {
    if (!(selectedEnchantments.value.includes('Light') && enchantment === 'Dark') && 
        !(selectedEnchantments.value.includes('Dark') && enchantment === 'Light')) {
      if (selectedEnchantments.value.length < 3) {
        selectedEnchantments.value.push(enchantment)
      }
    }
  }
}

const getWeaponImage = () => {
  if (!selectedWeapon.value) return ''
  const prefix = selectedWeapon.value.prefix
  const enchantmentCode = selectedEnchantments.value.map(e => e[0]).sort().join('')
  return `/images/${prefix}${enchantmentCode}.png`
}

const resetSelection = () => {
  selectedWeapon.value = null
  selectedEnchantments.value = []
}
</script>

<style scoped>
.carousel {
  display: flex;
  overflow: hidden;
  scroll-snap-type: x mandatory;
  scroll-behavior: smooth;
}
.carousel-item {
  flex: none;
  width: 100%;
  scroll-snap-align: start;
}
.cursor-pointer {
  cursor: pointer;
}
.selected-weapon {
  text-align: center;
  margin-top: 20px;
}
.btn {
  background-color: #3498db;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background 0.3s;
}
.btn:hover {
  background-color: #2980b9;
}
.enchantment-btn {
  margin: 5px;
}
.selected {
  background-color: #2ecc71;
}
</style>
