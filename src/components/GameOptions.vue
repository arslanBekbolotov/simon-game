<template>
  <div class="game-options">
    <h2>Уровень сложности:</h2>
    <div
      class="game-options__item"
      v-for="option in options"
      :key="option.value"
    >
      <input
        class="game-options__radio"
        type="radio"
        :name="option.name"
        :value="option.value"
        :checked="option.value === value"
        @change="$emit('input', option.value)"
      />
      {{ option.label }}
    </div>
  </div>
</template>
<script>
export default {
  props: {
    value: Number,
    options: {
      type: Array,
      required: true,
    },
  },
  data: () => {},
};
</script>
<style scoped>
.game-options {
  display: flex;
  flex-direction: column;
  align-items: baseline;
  margin-top: 20px;
}
</style>
