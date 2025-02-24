// HomeView.vue
<template>
  <div class="game-container">
    <h1 class="game-title" v-if="stage === 0">Build-A-Weapon</h1>
    <button v-if="stage === 0" @click="startGame" class="start-button">Start</button>
    <WeaponSelection v-if="stage === 1" @selectWeapon="selectWeapon" />
    <EnchantmentSelection v-if="stage >= 2 && stage <= 4" :weapon="selectedWeapon" :selectedEnchants="selectedEnchants" :stage="stage" @selectEnchant="selectEnchant" @nextStage="nextStage" @finishGame="finishGame" />
    <FinalDisplay v-if="stage === 5" :weapon="selectedWeapon" :enchants="selectedEnchants" @restartGame="restartGame" />
  </div>
</template>

<script>
import WeaponSelection from '@/components/WeaponSelection.vue';
import EnchantmentSelection from '@/components/EnchantmentSelection.vue';
import FinalDisplay from '@/components/FinalDisplay.vue';

export default {
  components: { WeaponSelection, EnchantmentSelection, FinalDisplay },
  data() {
    return {
      stage: 0,
      selectedWeapon: null,
      selectedEnchants: []
    };
  },
  methods: {
    startGame() {
      this.stage = 1;
    },
    selectWeapon(weapon) {
      this.selectedWeapon = weapon;
      this.stage = 2;
    },
    selectEnchant(enchant) {
      if (!this.selectedEnchants.includes(enchant.name) &&
          !(enchant.name === 'Light' && this.selectedEnchants.includes('Dark')) &&
          !(enchant.name === 'Dark' && this.selectedEnchants.includes('Light'))) {
        this.selectedEnchants[this.stage - 2] = enchant.name;
      }
    },
    nextStage() {
      if (this.selectedEnchants[this.stage - 2]) {
        if (this.stage < 5) {
          this.stage++;
        }
      }
    },
    finishGame() {
      this.stage = 5;
    },
    restartGame() {
      this.stage = 0;
      this.selectedWeapon = null;
      this.selectedEnchants = [];
    }
  }
};
</script>

<style>

.start-button{
  font-family: "Handjet", sans-serif;
  font-optical-sizing: auto;
}

.game-container {
  background: rgba(222, 184, 135, 0.7);
  padding: 40px;
  border-radius: 15px;
  text-align: center;
  width: 60%;
  margin: auto;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.game-title {
  font-family: "Handjet", sans-serif;
  font-optical-sizing: auto;
  font-size: 3rem;
  margin-bottom: 30px;
}
.start-button {
  background-color: orange;
  padding: 20px 40px;
  border: none;
  border-radius: 15px;
  cursor: pointer;
  font-size: 2rem;
  display: block;
  margin: 0 auto;
}

</style>
