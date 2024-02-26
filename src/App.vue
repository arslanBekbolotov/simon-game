<template>
  <div id="app">
    <h2>Simon Game</h2>
    <div class="content">
      <game-board
        :status.sync="status"
        :difficulty="difficulty"
        :round="round"
      />
      <div>
        <game-info
          :status="status"
          :round="round"
          @start-game="startGame"
          :last-round="lastRound"
        />
        <game-options :options="options" v-model="difficulty" />
      </div>
    </div>
  </div>
</template>

<script>
import GameOptions from "@/components/GameOptions.vue";
import GameBoard from "@/components/GameBoard.vue";
import GameInfo from "@/components/GameInfo.vue";

export default {
  name: "App",
  components: { GameInfo, GameBoard, GameOptions },
  data: () => ({
    status: "disabled",
    round: 0,
    lastRound: 0,
    difficulty: 1500,
    options: [
      {
        label: "Легкий",
        name: "easy",
        value: 1500,
      },
      {
        label: "Средний",
        name: "medium",
        value: 1000,
      },
      {
        label: "Сложный",
        name: "hard",
        value: 400,
      },
    ],
  }),
  watch: {
    status(val) {
      if (val === "win") this.nextRound();
      else if (val === "failed") this.failed();
    },
  },
  methods: {
    startGame() {
      this.round = 1;
      this.status = "run";
    },
    nextRound() {
      this.round++;
      this.status = "next";
    },
    failed() {
      this.lastRound = this.round;
      this.round = 0;
      this.status = "failed";
    },
  },
};
</script>

<style lang="scss">
.content {
  margin: auto;
  width: fit-content;
}
</style>
