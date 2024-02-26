<template>
  <div id="app">
    <game-options :options="options" v-model="difficulty" />
  </div>
</template>

<script>
import GameOptions from "@/components/GameOptions.vue";

export default {
  name: "App",
  components: { GameOptions },
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
};
</script>

<style lang="scss"></style>
