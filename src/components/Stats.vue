<template>
  <div class="block">
    <p>Your highest score is:</p>
    <p id="score">{{ bestScore }}</p>
    <p>Your average score is:</p>
    <p id="score">{{ avgScore }}</p>
  </div>
</template>

<script setup>
// PROPS
const props = defineProps({
  highestRank: {
    type: String,
  },
  bestScore: {
    type: String,
  },
  avgScore: {
    type: String,
  },
});
</script>

<style scoped>
.block {
  justify-content: center;
  align-items: center;
  background: rgb(128, 0, 96);
  color: white;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  font-size: 20px;
  font-weight: bold;
  margin: 20px 100px;
  padding: 80px 50px;
  border-radius: 25px;
}

p {
  color: rgb(169, 235, 255);
  font-size: 30px;
  font-weight: bold;
  margin: 10px 0;
}

#score {
  color: rgb(255, 255, 255);
  font-size: 40px;
  font-style: italic;
}
</style>
