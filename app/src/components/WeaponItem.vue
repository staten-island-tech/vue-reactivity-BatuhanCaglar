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
      <img :src="selectedWeapon.image" :alt="selectedWeapon.name" class="w-full" />
      <h2 class="text-center text-xl font-bold">{{ selectedWeapon.name }}</h2>
      <button @click="selectedWeapon = null" class="btn mt-4">Back</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const weapons = [
  { name: 'Greataxe', image: '/AXE.png' },
  { name: 'Longsword', image: '/SWORD.png' },
  { name: 'Scythe', image: '/SCYTHE.png' },
  { name: 'Mace', image: '/MACE.png' },
  { name: 'Spear', image: '/NAGINATA.png' },
]

const selectedWeapon = ref(null)

const selectWeapon = (weapon) => {
  selectedWeapon.value = weapon
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
</style>
