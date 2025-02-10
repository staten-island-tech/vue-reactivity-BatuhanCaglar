<template>
  <h1>Make-A-Weapon</h1>
  <div class="home-container">
    <button v-if="!gameStarted" @click="startGame" class="start-button">Start Game</button>

    <WeaponList v-if="gameStarted" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import WeaponList from '@/components/WeaponList.vue'

const gameStarted = ref(false)

const startGame = () => {
  gameStarted.value = true
}
</script>

<style scoped>
h1 {
  text-align: center;
  font-size: 7rem;
  font-family: 'Handjet', sans-serif;
  font-optical-sizing: auto;
}

.home-container {
  text-align: center;
  margin-top: 50px;
}

.start-button {
  background-color: #3498db;
  color: white;
  font-size: 20px;
  padding: 12px 24px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.3s;
}

.start-button:hover {
  background-color: #2980b9;
}

<div class="carousel w-full">
  <div id="item1" class="carousel-item w-full">
    <img
      src="https://img.daisyui.com/images/stock/photo-1625726411847-8cbb60cc71e6.webp"
      class="w-full" />
  </div>
  <div id="item2" class="carousel-item w-full">
    <img
      src="https://img.daisyui.com/images/stock/photo-1609621838510-5ad474b7d25d.webp"
      class="w-full" />
  </div>
  <div id="item3" class="carousel-item w-full">
    <img
      src="https://img.daisyui.com/images/stock/photo-1414694762283-acccc27bca85.webp"
      class="w-full" />
  </div>
  <div id="item4" class="carousel-item w-full">
    <img
      src="https://img.daisyui.com/images/stock/photo-1665553365602-b2fb8e5d1707.webp"
      class="w-full" />
  </div>
</div>
<div class="flex w-full justify-center gap-2 py-2">
  <a href="#item1" class="btn btn-xs">1</a>
  <a href="#item2" class="btn btn-xs">2</a>
  <a href="#item3" class="btn btn-xs">3</a>
  <a href="#item4" class="btn btn-xs">4</a>
</div>
</style>
