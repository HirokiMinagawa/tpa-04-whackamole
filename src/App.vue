<template>
  <div class="whackamole">
    <h1 class="logo">
      Whack-a-mole!
    </h1>
    <button
      @click="startGame"
      class="start-game"
      :disabled="duringGame"
    >
      Start Game
    </button>
    <div class="counters-container">
      <Counter title = "SCORE:" :number = "score" ></Counter>
      <Counter title = "HIGH SCORE:" :number = "highscore" ></Counter>
      <Counter title = "Time" :number = "time" ></Counter>
    </div>
    <div class="moles-container gameActive">
        <Mole v-for="(active, index) in moleData" :active = "active" :key="index" @moleClicked="moleClicked"></Mole>
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
      score: 0,
      highscore: 0,
      time: 20,
      moleData: [false, false, false, false],
      timerIntervalId: 0,
      moleIntervalId: 0,
      duringGame: false,
    };
  },
  methods: {
    startGame: function() {
      this.resetData();
      this.startTimer();
      this.startMoles();
    },
    startTimer: function() {
      this.timerIntervalId = setInterval(this.reduceTimer, 1000);
    },
    reduceTimer: function() {
      if (this.time > 0) {
        this.time -= 1;
      } else {
        this.stopTimer();
      }
    },
    stopTimer: function() {
      clearInterval(this.timerIntervalId);
      this.stopMoles();
    },
    moleClicked: function() {
      this.addScore();
    },
    addScore: function() {
      this.score += 1;
    },
    resetData: function() {
      this.score = 0;
      this.time = 20;
      this.timerIntervalId= 0;
      this.duringGame = true;
      this.resetMoleData();
    },
    startMoles: function() {
      this.moleIntervalId = setInterval(this.reverseRandomMoleStatus, 50);
    },
    reverseRandomMoleStatus: function() {
      const randomIndex = Math.floor(Math.random() * this.moleData.length);
      this.moleData[randomIndex] = !this.moleData[randomIndex];
    },
    stopMoles: function() {
      clearInterval(this.moleIntervalId);
      this.resetMoleData();
      this.endGame();
    },
    endGame: function() {
      this.updateHighScore();
      this.duringGame = false;
    },
    updateHighScore: function() {
      if (this.score > this.highscore) {
        this.highscore = this.score;
      }
    },
    resetMoleData: function() {
      this.moleData = this.moleData.map(() => false);
    }
  },
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
