<template>
  <div id="app">
    <h2>Simon Game</h2>
    <div>
      <game-board
        :status.sync="status"
        :difficulty="difficulty"
        :round="round"
        @tile-clicked="tileClicked"
      />
      <game-options :options="options" v-model="difficulty" />
    </div>
  </div>
</template>

<script>
import GameOptions from "@/components/GameOptions.vue";
import GameBoard from "@/components/GameBoard.vue";

export default {
  name: "App",
  components: { GameBoard, GameOptions },
  data: () => ({
    status: "disabled",
    round: 0,
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
  methods: {
    tileClicked() {},
  },
};
</script>

<style lang="scss"></style>
