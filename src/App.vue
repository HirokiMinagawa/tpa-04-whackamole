<template>
  <div class="whackamole">
    <h1 class="logo">
      Whack-a-mole!
    </h1>
    <button
      class="start-game"
    >
      Start Game
    </button>
    <div class="counters-container">
      <Counter title = "SCORE:" :number = "score" ></Counter>
      <Counter title = "HIGH SCORE:" :number = "highscore" ></Counter>
      <Counter title = "Time" :number = "time" ></Counter>
    </div>
    <div class="moles-container gameActive">
      <div v-for="n in moleData" :key="n">
        <Mole :isActive = "isActive" :isInActive = "isInActive"></Mole>
      </div>
    </div>
  </div>
</template>

<script>
import Counter from './components/Counter.vue';
import Mole from './components/Mole.vue';

export default {
  name: 'App',
  components: {
    Counter: Counter,
    Mole: Mole,
  },
  data: function() {
    return {
      score: 100,
      highscore: 300,
      time: 10,
      status: false,
      isActive: true,
      isInActive: false,
      moleData: 4,
    };
  }
};
</script>

<style>
.whackamole {
  font-family: 'Bungee', sans-serif;
  max-width: 960px;
  margin: auto;
  text-align: center;
}

.start-game {
  font-family: 'Bungee', sans-serif;
  padding: 20px;
  border-radius: 3px;
  border: 0;
  background-color: #52b1d6;
  color: #fff;
  font-size: 1em;
  cursor: pointer;
}

.counters-container {
  display: flex;
  justify-content: space-evenly;
}

.moles-container {
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
  opacity: 0.5;
  transition: opacity 0.3s ease;
}

.moles-container.game-active {
  opacity: 1;
}
</style>
