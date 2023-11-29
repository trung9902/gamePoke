<template>
  <div class="result">
    <h1 class="result__title">✨ Congratulations ✨</h1>
    <h3 class="result__rank">{{ Math.round(timer / 1000) }} seconds</h3>
    <button @click="onStartAgain()">Start Again</button>
  </div>
</template>

<script>
export default {
  props: {
    timer: {
      type: Number,
      reqired: true,
    },
  },
  methods: {
    onStartAgain() {
      this.$emit("handerScreen");
    },
  },
};
</script>

<style scoped>
.result {
  height: 94vh;
  background-color: var(--dark);
  color: var(--light);
}

.result h3 {
  font-size: 48px;
  font-weight: 700;
  padding-top: 20px;
  padding-bottom: 20px;
}
.result button {
  font-family: "Odibee Sans", sans-serif;
  width: 108px;
  height: 55px;
  font-size: 16px;
  text-align: center;
  background-color: var(--dark);
  border: 1px solid var(--light);
  border-radius: 8px;
  color: var(--light);
  transition: 0.3s ease-in-out 0s;
}
.result button:hover {
  background-color: var(--light);
  color: var(--dark);
  cursor: pointer;
}
.result__title {
  padding-top: 15%;
  font-size: 80px;
}
</style>
