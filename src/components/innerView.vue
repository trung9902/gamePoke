<template>
  <div class="screen">
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((920 - 16 * 4) / Math.sqrt(cardsContent.length) - 16) * 3) / 4 +
            16) *
          Math.sqrt(cardsContent.length)
        }px`,
      }"
    >
      <card-poken
        v-for="(card, index) in cardsContent"
        :key="index"
        :ref="`card-${index}`"
        :imgBackFaceUrl="`image/${card}.png`"
        :card="{ index: index, value: card }"
        @onFlip="onHanderpush($event)"
        :cardsContent="cardsContent"
      />
    </div>
  </div>
</template>
<script>
import cardPoken from "./cardPoken.vue";
export default {
  props: {
    cardsContent: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      rulel: [],
    };
  },
  methods: {
    onHanderpush(card) {
      console.log(card);
      if (this.rulel.length === 2) return false;
      this.rulel.push(card);
      console.log(this.rulel);
      if (
        this.rulel.length === 2 &&
        this.rulel[0].value === this.rulel[1].value
      ) {
        console.log("right....");
        this.$refs[`card-${this.rulel[0].index}`][0].onFlipDisable();
        this.$refs[`card-${this.rulel[1].index}`][0].onFlipDisable();
        // reset reles
        this.rulel = [];
        const disabledElement = document.querySelectorAll(".screen .disabled");
        if (
          disabledElement &&
          disabledElement.length === this.cardsContent.length - 2
        ) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 900);
        }
      } else if (
        this.rulel.length === 2 &&
        this.rulel[0].value !== this.rulel[1].value
      ) {
        console.log("wrong....");
        setTimeout(() => {
          this.$refs[`card-${this.rulel[0].index}`][0].onFlipBack();
          this.$refs[`card-${this.rulel[1].index}`][0].onFlipBack();
          this.rulel = [];
        }, 600);
      } else return false;
    },
  },
  components: { cardPoken },
};
</script>
<style lang="css" scoped>
.screen {
  text-align: center;
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}
.screen__inner {
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
