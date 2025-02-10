<template>
  <div class="weapon-list">
    <WeaponCard v-for="weapon in weapons" :key="weapon.name" :weapon="weapon" />
  </div>
</template>

<script setup>
import WeaponCard from '@/components/WeaponCard.vue'

const weapons = [
  { name: 'Greataxe', image: '/download-removebg-preview(1).png' },
  { name: 'Longsword', image: '/download-removebg-preview.png' },
  { name: 'Scythe', image: '/download-removebg-preview(3).png' },
  { name: 'Mace', image: '/download-removebg-preview(2).png' },
  { name: 'Spear', image: '/images-removebg-preview.png' },
]
</script>

<style scoped>
.weapon-list {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  justify-content: center;
}
</style>
