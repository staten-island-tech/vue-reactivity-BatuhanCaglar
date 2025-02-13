<template>
  <div class="home-container">
    <button v-if="!gameStarted" @click="startGame" class="start-button">Start Game</button>

    <WeaponList v-if="gameStarted" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import WeaponList from '@/components/WeaponItem.vue'

// Reactive state to track if the game has started
const gameStarted = ref(false)

// Function to start the game
const startGame = () => {
  gameStarted.value = true
}
</script>

<style scoped>
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
</style>