<template>
  <div class="block">
    <p id="message">{{ data.message }}</p>
    <p>Your reaction time was {{ score }} ms</p>
  </div>
</template>

<script setup>
// IMPORTS
import { ref, onMounted, reactive } from "vue";

// PROPS
const props = defineProps({
  score: {
    type: Number,
  },
});

// MESSAGE
const data = reactive({
  message: null,
});

// HOOKS
onMounted(() => {
  if (props.score < 220) {
    data.message = "WOW!";
  } else if (props.score < 300) {
    data.message = "That's pretty good!";
  } else if (props.score < 400) {
    data.message = "Meh. Average";
  } else if (props.score < 500) {
    data.message = "Come on. You can do better";
  } else {
    data.message = "Ok. That's pretty trash";
  }
});
</script>

<style scoped>
.block {
  justify-content: center;
  align-items: center;
  background: rgb(0, 113, 128);
  color: white;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  font-size: 20px;
  font-weight: bold;
  margin: 20px 100px;
  padding: 80px 50px;
  border-radius: 25px;
}

#message {
  color: antiquewhite;
  font-size: 40px;
  font-weight: bold;
  margin: 10px 0;
}
</style>
