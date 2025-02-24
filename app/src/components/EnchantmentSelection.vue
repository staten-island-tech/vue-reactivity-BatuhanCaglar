<template>
    <div class="enchantment-selection">
      <h2>Select Your Enchantments</h2>
      <h3>Chosen Weapon: {{ weapon.name }}</h3>
  
      <div v-if="selectedEnchants.length" class="chosen-enchants">
        <h4>Chosen Enchants:</h4>
        <div class="enchant-list">
          <span v-for="enchant in selectedEnchants" :key="enchant" class="chosen-enchant">{{ enchant }}</span>
        </div>
      </div>
  
      <div class="enchantment-options">
        <div v-for="enchant in filteredEnchantments" :key="enchant.name" class="enchant-option">
          <img :src="enchant.image" :alt="enchant.name" class="enchant-image" />
          <button @click="$emit('selectEnchant', enchant)" class="enchant-button">{{ enchant.name }}</button>
        </div>
      </div>
  
      <div class="button-container">
        <button v-if="stage < 4" @click="$emit('nextStage')" class="next-button" :disabled="!selectedEnchants[stage - 2]">Next</button>
        <button @click="$emit('finishGame')" class="finish-button">Finish</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['weapon', 'selectedEnchants', 'stage'],
    computed: {
      filteredEnchantments() {
        return this.enchantments.filter(enchant => 
          !this.selectedEnchants.includes(enchant.name) && 
          !((enchant.name === 'Light' && this.selectedEnchants.includes('Dark')) || 
            (enchant.name === 'Dark' && this.selectedEnchants.includes('Light')))
        );
      }
    },
    data() {
      return {
        enchantments: [
          { name: 'Fire', image: '/fireballpic.webp' },
          { name: 'Wind', image: '/windpic.png' },
          { name: 'Dark', image: '/darkball.png' },
          { name: 'Light', image: '/lightball.png' },
          { name: 'Lightning', image: '/lightbolt.png' }
        ]
      };
    }
  };
  </script>
  
  <style>
 h3{
    font-family: "Handjet", sans-serif;
  font-optical-sizing: auto;
  font-size: xx-large;
 }

  .enchantment-selection {
    text-align: center;
  }
  .chosen-enchants {
    margin-bottom: 15px;
    font-family: "Rajdhani", sans-serif;
    font-weight: 600;
    font-style: normal;
  }
  .enchant-list {
    display: flex;
    justify-content: center;
    gap: 10px;
    font-family: "Rajdhani", sans-serif;
    font-weight: 400;
    font-style: normal;
  }
  .enchant-option {
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: center;
    font-family: "Rajdhani", sans-serif;
    font-weight: 400;
    font-style: normal;
  }
  .enchantment-options {
    display: flex;
    justify-content: center;
    gap: 20px;
    flex-wrap: wrap;
  }
  .enchant-image {
    width: 20px;
    height: auto;
    border-radius: 50%;
  }
  .enchant-button {
    background-color: orange;
    border: none;
    padding: 10px;
    margin-top: 5px;
    cursor: pointer;
    font-size: 1rem;
    font-family: "Rajdhani", sans-serif;
    font-weight: 500;
    font-style: normal;
  }
  .button-container {
    margin-top: 20px;
    display: flex;
    justify-content: center;
    gap: 15px;
  }
  .next-button, .finish-button {
    background-color: orange;
    padding: 15px;
    border: none;
    cursor: pointer;
    font-size: 1.2rem;
    font-family: "Rajdhani", sans-serif;
    font-weight: 600;
    font-style: normal;
  }
  </style>
  