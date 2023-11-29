<template>
  <div
    class="card"
    :class="{ disabled: isDisable }"
    :style="{
      height: `${(920 - 16 * 4) / Math.sqrt(cardsContent.length) - 16}px`,
      width: `${
        (((920 - 16 * 4) / Math.sqrt(cardsContent.length) - 16) * 3) / 4
      }px`,
      perspective: `${
        ((((920 - 16 * 4) / Math.sqrt(cardsContent.length) - 16) * 3) / 4) * 2
      }px`,
    }"
  >
    <div
      class="card-inner"
      :class="{ 'is-flipped': isFlipped }"
      @click="onToggleClick()"
    >
      <div class="card__face card__face-front">
        <div
          class="card__content"
          :style="{
            backgroundSize: `${
              (((920 - 16 * 4) / Math.sqrt(cardsContent.length) - 16) * 3) /
              4 /
              3
            }px ${
              (((920 - 16 * 4) / Math.sqrt(cardsContent.length) - 16) * 3) /
              4 /
              3
            }px `,
          }"
        ></div>
      </div>
      <div class="card__face card__face-back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + imgBackFaceUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    card: {
      typeof: [String, Number, Array, Object],
    },
    imgBackFaceUrl: {
      type: String,
      require: true,
    },
    cardsContent: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      isFlipped: false,
      isDisable: false,
    };
  },
  methods: {
    onToggleClick() {
      // console.log(this.isFlipped);
      if (this.isDisable) return false;
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) this.$emit("onFlip", this.card);
    },
    onFlipBack() {
      // console.log("ssss");
      this.isFlipped = false;
    },
    onFlipDisable() {
      this.isDisable = true;
    },
  },
};
</script>
<style scoped>
.card {
  width: 90px;
  height: 120px;
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
}
.card.disabled {
  cursor: default;
}
.card-inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
}
.card-inner.is-flipped {
  transform: rotateY(-180deg);
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}
.card__face-front .card__content {
  background: url("../assets/image/icon_back.png") no-repeat center center;
  height: 100%;
  width: 100%;
}
.card__face-back {
  background-color: #f3f3f3;
  transform: rotateY(-180deg);
}
.card__face-back .card__content {
  width: 100%;
  height: 100%;
  background-repeat: no-repeat;
  background-position: center center;
  background-size: contain;
}
</style>
