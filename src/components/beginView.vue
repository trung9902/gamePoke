<template>
  <div class="screen__begin">
    <div class="begin-tittle">
      <h1 class="tittle">POKE MEMORIES</h1>
      <p class="begin__des">Select mode to start game</p>
    </div>
    <div class="button">
      <button @click="onSelectMode(16)" class="btn button__leve1">
        <span>4x4</span>
        <p>Easy</p>
      </button>
      <button @click="onSelectMode(32)" class="btn button__leve2">
        <span>6x6</span>
        <p>Normal</p>
      </button>
      <button @click="onSelectMode(64)" class="btn button__leve3">
        <span>8x8</span>
        <p>Hard</p>
      </button>
      <button @click="onSelectMode(100)" class="btn button__leve4">
        <span>10x10</span>
        <p>Super Hard</p>
      </button>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    onSelectMode(total) {
      this.$emit("onstart", { total });
    },
  },
};
</script>
<style scoped>
.screen__begin {
  height: 94vh;
  background-color: var(--dark);
  color: var(--light);
}
.begin-tittle {
  padding-top: 15%;
}
.tittle {
  font-size: 72px;
  font-weight: 700;
}
.begin__des {
  font-size: 32px;
}
.button {
  margin-top: 30px;
  display: flex;
  justify-content: center;
  gap: 30px;
}
.btn {
  font-family: "Odibee Sans", sans-serif;
  width: 150px;
  height: 150px;
  font-size: 16px;
  text-align: center;
  background-color: var(--dark);
  border: 1px solid var(--light);
  border-radius: 22px;
  color: var(--light);
  transition: 0.3s ease-in-out 0s;
}
.btn:hover {
  background-color: var(--light);
  color: var(--dark);
  cursor: pointer;
}
.btn span {
  font-size: 32px;
}
.btn p {
  font-size: 20px;
}
</style>
