<template>
  <div>
    <!-- Weapon Selection -->
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

    <!-- Selected Weapon & Enchantment Selection -->
    <div v-if="selectedWeapon && !isFinished" class="selected-weapon animate-fade-scale">
      <h2 class="text-center text-xl font-bold">Selected: {{ selectedWeapon.name }}</h2>
      <img :src="getWeaponImage()" :alt="selectedWeapon.name" class="w-full transition-image" />

      <!-- Display Current Enchantments -->
      <div class="selected-enchantments animate-fade-scale">
        <h3>Current Enchantments:</h3>
        <span v-if="selectedEnchantments.length === 0">None</span>
        <span v-for="enchantment in selectedEnchantments" :key="enchantment" class="badge">{{
          enchantment
        }}</span>
      </div>

      <!-- Enchantment Selection -->
      <div
        v-if="currentStage <= 3 && availableEnchantments.length > 0"
        class="enchantments animate-fade-scale"
      >
        <h3>Select an Enchantment (Stage {{ currentStage }}):</h3>
        <button
          v-for="enchantment in availableEnchantments"
          :key="enchantment"
          @click="selectEnchantment(enchantment)"
          class="btn enchantment-btn"
        >
          {{ enchantment }}
        </button>
      </div>

      <!-- Next Button -->
      <div
        v-if="
          selectedEnchantments.length === currentStage &&
          currentStage < 3 &&
          availableEnchantments.length > 0
        "
        class="controls"
      >
        <button @click="nextStage" class="btn mt-4 transition-scale">Next</button>
      </div>

      <!-- Finish Selection -->
      <div v-if="selectedEnchantments.length > 0" class="controls">
        <button @click="finishSelection" class="btn mt-4 transition-scale">Finish</button>
      </div>

      <!-- Restart Button -->
      <div class="controls">
        <button @click="resetSelection" class="btn mt-4 transition-scale">Restart</button>
      </div>
    </div>

    <!-- Final Selection Display -->
    <div v-if="isFinished" class="final-selection animate-fade-scale">
      <h2 class="text-center text-xl font-bold">Final Selection</h2>
      <p>Weapon: {{ selectedWeapon.name }}</p>
      <p>
        Enchantments:
        <span v-if="selectedEnchantments.length === 0">None</span>
        <span v-for="enchantment in selectedEnchantments" :key="enchantment" class="badge">{{
          enchantment
        }}</span>
      </p>
      <img :src="getWeaponImage()" :alt="selectedWeapon.name" class="final-image" />

      <!-- Restart Button -->
      <div class="controls">
        <button @click="resetSelection" class="btn mt-4 transition-scale">Restart</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const weapons = [
  { name: 'Greataxe', prefix: 'A', image: '/AXE.png' },
  { name: 'Longsword', prefix: 'S', image: '/SWORD.png' },
  { name: 'Scythe', prefix: 'Y', image: '/SCYTHE.png' },
  { name: 'Mace', prefix: 'M', image: '/MACE.png' },
  { name: 'Naginata', prefix: 'P', image: '/NAGINATA.png' },
]

const allEnchantments = ['Dark', 'Light', 'Fire', 'Wind', 'Lightning']
const selectedWeapon = ref(null)
const selectedEnchantments = ref([])
const currentStage = ref(1)
const isFinished = ref(false)

const availableEnchantments = computed(() => {
  return allEnchantments.filter(
    (e) =>
      !selectedEnchantments.value.includes(e) &&
      !(selectedEnchantments.value.includes('Light') && e === 'Dark') &&
      !(selectedEnchantments.value.includes('Dark') && e === 'Light'),
  )
})

const selectWeapon = (weapon) => {
  selectedWeapon.value = weapon
  selectedEnchantments.value = []
  currentStage.value = 1
  isFinished.value = false
}

const selectEnchantment = (enchantment) => {
  if (selectedEnchantments.value.length === currentStage.value - 1) {
    selectedEnchantments.value.push(enchantment)
  }
}

const nextStage = () => {
  if (currentStage.value < 3) {
    currentStage.value++
  }
}

const finishSelection = () => {
  isFinished.value = true
}

const getWeaponImage = () => {
  if (!selectedWeapon.value) return ''
  const prefix = selectedWeapon.value.prefix
  const enchantmentCode = selectedEnchantments.value
    .map((e) => e[0])
    .sort()
    .join('')
  return `/images/${prefix}${enchantmentCode}.png`
}

const resetSelection = () => {
  selectedWeapon.value = null
  selectedEnchantments.value = []
  currentStage.value = 1
  isFinished.value = false
}
</script>

<style scoped>
.animate-fade-scale {
  animation: fadeScale 0.5s ease-in-out;
}

@keyframes fadeScale {
  from {
    opacity: 0;
    transform: scale(0.9);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

.transition-scale {
  transition: transform 0.2s;
}
.transition-scale:active {
  transform: scale(0.95);
}

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
.selected-weapon,
.final-selection {
  text-align: center;
  margin-top: 20px;
}
.selected-enchantments,
.final-selection {
  margin-top: 10px;
  font-size: 1.1em;
}
.badge {
  display: inline-block;
  background-color: #e67e22;
  color: white;
  padding: 5px 10px;
  margin: 5px;
  border-radius: 5px;
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
set .btn:disabled {
  background-color: #95a5a6;
  cursor: not-allowed;
}
.enchantment-btn {
  margin: 5px;
}
.transition-image {
  transition: opacity 0.5s ease-in-out;
}
.final-image {
  width: 300px;
  height: auto;
  margin-top: 20px;
}
</style>
