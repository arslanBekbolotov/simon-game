<template>
  <div
    class="section"
    :class="[section.active && 'active', section.color]"
  ></div>
</template>

<script>
export default {
  props: {
    section: {
      type: Object,
      required: true,
    },
    status: {
      type: String,
    },
  },
};
</script>

<style lang="scss" scoped>
.section {
  opacity: 0.6 !important;
  transition: opacity 250ms ease;
}

.active {
  opacity: 1 !important;
}

.red,
.blue,
.yellow,
.green {
  height: 290px;
  position: absolute;
}

.red {
  background: #ff5643;
  clip: rect(0px, 300px, 150px, 150px);
  width: 296px;
}

.blue {
  background: dodgerblue;
  clip: rect(0px, 150px, 150px, 0px);
  width: 300px;
}

.yellow {
  background: #feef33;
  clip: rect(150px, 150px, 300px, 0px);
  width: 300px;
}

.green {
  background: #bede15;
  clip: rect(150px, 300px, 300px, 150px);
  width: 296px;
}
</style>
