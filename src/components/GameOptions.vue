<template>
  <div class="game-options">
    <h2 class="game-options__title">Уровень сложности:</h2>
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
};
</script>
<style lang="scss" scoped>
.game-options {
  display: flex;
  flex-direction: column;
  align-items: baseline;
  margin-top: 20px;

  &__title {
    margin-top: 30px;
  }

  &__radio {
    margin-bottom: 10px;
  }
}
</style>
