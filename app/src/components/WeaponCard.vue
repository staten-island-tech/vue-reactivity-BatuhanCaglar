<template>
  <div class="card">
    <img :src="weapon.image" :alt="weapon.name" class="weapon-image" />
    <h3>{{ weapon.name }}</h3>
  </div>
</template>

<script setup>
defineProps({
  weapon: Object,
})
</script>

<style scoped>
.card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 16px;
  text-align: center;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
  background: #fff;
  transition: transform 0.2s;
  width: 200px;
}

.card:hover {
  transform: scale(1.05);
}

.weapon-image {
  width: 100%;
  height: auto;
  border-radius: 8px;
}
</style>
