<template>
  <begin-view
    v-if="status === 'default'"
    @onstart="onHanderBeforeStart($event)"
  />
  <inner-view
    v-if="status === 'math'"
    :cardsContent="settings.cardsContent"
    @onFinish="onGetResult"
  />
  <result-component
    v-if="status === 'result'"
    :timer="timer"
    @handerScreen="status = 'default'"
  />
  <footer>
    <footer-view />
  </footer>
</template>

<script>
import innerView from "./components/innerView.vue";
import BeginView from "./components/beginView.vue";
import FooterView from "./components/footerView.vue";
import ResultComponent from "./components/resultComponent.vue";

import { shuffled } from "./utils/array";
export default {
  name: "App",
  components: {
    BeginView,
    FooterView,
    innerView,
    ResultComponent,
  },
  data() {
    return {
      settings: {
        total: 0,
        cardsContent: [],
        starteAt: null,
      },
      status: "default",
      timer: 0,
    };
  },
  methods: {
    onHanderBeforeStart(config) {
      // data ready
      this.settings.total = config.total;
      const firstCards = Array.from(
        { length: this.settings.total / 2 },
        (_, i) => i + 1
      );
      const seconCards = [...firstCards];
      const Cards = [...firstCards, ...seconCards];
      this.settings.cardsContent = shuffled(
        shuffled(shuffled(shuffled(Cards)))
      );
      this.settings.starteAt = new Date().getTime();
      // console.log(this.settings.cardsContent);
      console.log(Cards);
      this.status = "math";
    },
    onGetResult() {
      // get timer
      this.timer = new Date().getTime() - this.settings.starteAt;
      // swich to result component
      this.status = "result";
    },
  },
};
</script>

<style scoped>
#app {
  font-family: "Odibee Sans", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
