<template>
  <div class="block" v-if="data.showBlock" @mousedown="stopCounter">
    <p>! NOW !</p>
  </div>
</template>

<script setup>
// IMPORTS
import { reactive, onMounted } from "vue";
// DATA
const data = reactive({
  showBlock: false,
  timer: null,
  reactionTime: 0,
});

// PROPS & EMITS
const props = defineProps({
  gameOn: {
    type: Boolean,
  },
  delay: {
    type: Number,
  },
});

const emits = defineEmits(["close"]);

// MOUNTED DELAY
onMounted(() => {
  setTimeout(() => {
    data.showBlock = true;
    startCounter();
  }, props.delay);
});

// REACTION TIMER
const startCounter = () => {
  data.timer = setInterval(() => {
    data.reactionTime += 10;
  }, 10);
};
const stopCounter = () => {
  clearInterval(data.timer);
  emits("close", data.reactionTime);
};
</script>

<style scoped>
.block {
  display: flex;
  justify-content: center;
  align-items: center;
  background: green;
  color: white;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  font-size: 40px;
  font-weight: bold;
  margin: 20px 100px;
  padding: 80px 50px;
  border-radius: 25px;
}
</style>
