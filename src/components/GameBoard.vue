<template>
  <div class="game-board">
    <div class="game-board__items">
      <game-board-section
        v-for="section in sections"
        :section="section"
        :key="section.id"
        :status="status"
        @section-clicked="sectionClicked"
        @change-activity="changeActivity"
      />
    </div>
  </div>
</template>
<script>
import GameBoardSection from "@/components/GameBoardSection.vue";

export default {
  props: {
    status: {
      type: String,
      required: true,
    },
    isDisabled: {
      type: Boolean,
      default: false,
    },
    round: {
      type: Number,
      required: true,
    },
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
  watch: {
    status(value) {
      if (value === "run") this.start();
      if (value === "next") this.run();
    },
  },
  methods: {
    sectionClicked(id) {
      this.userSequence.push(id);
      if (this.isFailed()) {
        this.$emit("update:status", "failed");
        this.userSequence = [];
        this.sequence = [];
      } else if (this.sequence.length === this.userSequence.length) {
        this.$emit("update:status", "win");
        this.userSequence = [];
      }
    },
    isFailed() {
      const length = this.userSequence.length;
      return this.sequence[length - 1] !== this.userSequence[length - 1];
    },
    async play() {
      for (const item of this.sequence) {
        const section = this.sections[item];
        await this.playSound(section);
      }
      this.$emit("update:status", "play");
    },
    async playSound(item) {
      return new Promise((resolve) => {
        setTimeout(() => {
          item.active = true;
          resolve();
        }, this.difficulty);
      });
    },
    start() {
      this.sequence = [];
      this.userSequence = [];
      this.run();
    },
    run() {
      let randomNum = this.getRandom();
      this.sequence.push(randomNum);
      this.play();
    },
    getRandom() {
      return Math.floor(Math.random() * 4);
    },
    changeActivity(id, newValue) {
      this.sections[id].active = newValue;
    },
  },
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
    border-radius: 10%;
    overflow: hidden;
    box-shadow: 2px 1px 12px #aaa;
  }
}
</style>
