<template>
  <div class="block">
    <p id="message">Your highest score is: {{ bestScore }}</p>
    <p>Your average score is: {{ avgScore }}</p>
  </div>
</template>

<script setup>
// PROPS
const props = defineProps({
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
  font-size: 40px;
  font-weight: bold;
  margin: 10px 0;
}
</style>
