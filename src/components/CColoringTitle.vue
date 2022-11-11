<template>
  <h3 class="c-coloring-title">
    <span v-for="(t, i) in text" :key="i">{{ t }}</span>
  </h3>
</template>

<script>

export default {
  props: {
    text: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style lang="scss">
.c-coloring-title {
  display: flex;
  flex-direction: column;
  margin: 0;
  font-weight: 500;
  letter-spacing: 2px;
  line-height: 1;
  font-size: 28px;

  span {
    margin: 0;
    align-self: flex-start;
    letter-spacing: 1px;

    @include coveredText($dark-color);

    @include BlockCoveringText($dark-color, 0.2s, 0.2s);
  }

  span:nth-child(2) {
    @include BlockCoveringText($dark-color, 0.2s, 0.3s);
  }

  span:nth-child(3) {
    @include BlockCoveringText($dark-color, 0.3s, 0.4s);
  }

  span + span {
    margin-top: 4px;
  }
}
</style>
