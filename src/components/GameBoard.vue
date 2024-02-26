<template>
  <div class="game-board">
    <div class="game-board__items">
      <game-board-section
        v-for="section in sections"
        :section="section"
        :key="section.id"
        :status="status"
      />
    </div>
  </div>
</template>
<script>
import GameBoardSection from "@/components/GameBoardSection.vue";

export default {
  props: {
    status: String,
    isDisabled: {
      type: Boolean,
      default: false,
    },
    round: Number,
    difficulty: {
      type: Number,
      required: true,
    },
  },
  components: {
    GameBoardSection,
  },
  data: () => ({
    sequence: [],
    userSequence: [],
    sections: [
      {
        id: 0,
        color: "red",
        active: false,
      },
      {
        id: 1,
        color: "blue",
        active: false,
      },
      {
        id: 2,
        color: "yellow",
        active: false,
      },
      {
        id: 3,
        color: "green",
        active: false,
      },
    ],
  }),
};
</script>

<style lang="scss" scoped>
.game-board {
  &__items {
    background: #fff;
    position: relative;
    float: left;
    margin-right: 3em;
    width: 295px;
    height: 285px;
    border-radius: 50%;
    overflow: hidden;
    box-shadow: 2px 1px 12px #aaa;
  }
}
</style>
