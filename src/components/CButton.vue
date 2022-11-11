<template>
  <button class="c-button" :class="{ light: light }">Read more</button>
</template>

<script>
export default {
  props: {
    light: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
};
</script>

<style lang="scss">
.c-button {
  padding: 25px 60px 25px 40px;
  font-size: 12px;
  line-height: 1;
  font-weight: 500;
  letter-spacing: 3px;
  text-transform: uppercase;
  background-color: #1b2a2f;
  color: #fff;
  border: none;
  white-space: nowrap;

  .light {
    background-color: transparent;
    border: 2px solid #1b2a2f;
    color: #1b2a2f;
  }
}
</style>
