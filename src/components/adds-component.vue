<template>
  <button class="button-add">
    <span class="visually-hidden">добавить секундомер</span>
  </button>
</template>
<script>
export default {
  name: 'addsStopwatch',
  data() {
    return {};
  },
  methods: {},
};
</script>
<style lang="scss">
.button-add {
  border: none;
  position: relative;
  min-height: 120px;
  outline: none;

  background-color: $stopwath-bkg;

  &:focus {
    outline: 1px solid $off-stopwath-color;
    outline-offset: 5px;
  }
  &::after {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 20px;
    height: 3px;
    background-color: $off-stopwath-color;
  }

  &::before {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) rotate(90deg);
    width: 20px;
    height: 3px;
    background-color: $off-stopwath-color;
  }
}
</style>
