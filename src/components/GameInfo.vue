<template>
  <div class="game-info">
    <h2>
      Раунд:
      <span>{{ round }}</span>
    </h2>
    <button
      @click="$emit('start-game')"
      class="game-info__btn"
      :disabled="isBtnDisabled"
    >
      Start
    </button>
    <p v-if="isFailed">
      Вы проиграли после <span>{{ round }}</span> раундов!
    </p>
  </div>
</template>
<script>
export default {
  props: {
    status: {
      type: String,
      required: true,
    },
    round: {
      type: Number,
      required: true,
    },
    lastRound: {
      type: Number,
      required: true,
    },
  },
  computed: {
    isFailed() {
      return this.status === "failed";
    },
    isBtnDisabled() {
      return this.status === "play" || this.status === "run";
    },
  },
};
</script>
<style lang="scss" scoped>
.game-info {
  text-align: start;

  &__btn {
    width: 5em;
    box-sizing: border-box;
    font-size: 1.4em;
    -webkit-border-radius: 10px 10px 10px 10px;
    border-radius: 10px 10px 10px 10px;
    background: #a7caef;
    border: none;
    padding: 0.3em 0.6em;
  }
}
</style>
