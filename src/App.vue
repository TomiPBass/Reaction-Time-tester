<template>
  <div>
    <h1>Reaction time tester!</h1>
    <div class="button">
      <button @click="startGame()" :disabled="data.gameOn">Play!</button>
    </div>
    <div class="button">
      <button class="stats" @click="showStats">{{ data.statsText }}</button>
    </div>
    <Block
      v-if="data.gameOn"
      :game-on="data.gameOn"
      :delay="data.delay"
      @close="closeGame"
    />
    <Results v-if="data.resultsOn" :score="data.score" />
    <Stats v-if="data.statsOn" :best-score="data.bestScore" :avg-score="data.avgScore" />
  </div>
</template>

<script setup>
// IMPORTS
import { reactive } from "vue";
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";
import Stats from "./components/Stats.vue";

// DATA
const data = reactive({
  gameOn: false,
  resultsOn: false,
  statsOn: false,
  statsText: "Show Stats",
  delay: null,
  score: null,
  bestScore: "!You have to play first!",
  avgScore: "!You have to play first!",
  highestRank: "!You have to play first!",
});

// STATS
let stats = [];
const computeStats = () => {
  stats.sort(function (a, b) {
    return a - b;
  });
  data.bestScore = stats[0] + "ms";
  data.avgScore =
    stats.reduce((total, stat) => {
      return total + stat;
    }) /
      stats.length +
    "ms";
};
const showStats = () => {
  data.statsOn = !data.statsOn;
  data.resultsOn = false;
  if (data.statsOn === true) {
    data.statsText = "Hide Stats";
  } else {
    data.statsText = "Show Stats";
  }
};

// GAME
const startGame = () => {
  data.delay = 2000 + Math.random() * 5000;
  data.resultsOn = false;
  data.gameOn = true;
  data.statsOn = false;
  data.statsText = "Show Stats";
};
const closeGame = (reactionTime) => {
  data.score = reactionTime;
  stats.push(data.score);
  console.log(stats);
  computeStats();
  data.gameOn = false;
  data.resultsOn = true;
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
  border-bottom: 1px solid #ddd;
  display: inline-block;
}
.button {
  display: flex;
  justify-content: center;
}
button {
  margin: 10px 30px;
  padding: 10px 20px;
  background: aquamarine;
  color: rgb(65, 65, 65);
  font-size: 20px;
  font-weight: bold;
  border: none;
  border-radius: 15px;
  cursor: pointer;
}
.stats {
  background: rgb(241, 65, 65);
  color: rgb(255, 255, 255);
}

button:disabled {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
