<template>
  <div id="app">
    <div class="wrapper">
      <div class="container">
        <div class="stopwatchs__container">
          <stopwatch />
          <stopwatch v-for="(stopwatch, index) in stopWatches" :key="index" :is="stopwatch" />
          <adds-component @click="addsStopwatch" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import stopwatch from './components/stopwatch.vue';
import addsComponent from './components/adds-component.vue';

export default {
  name: 'App',
  data() {
    return {
      stopWatches: [],
    };
  },
  components: {
    stopwatch,
    addsComponent,
  },
  methods: {
    addsStopwatch: function () {
      this.stopWatches.unshift(stopwatch);
    },
  },
};
</script>

<style lang="scss">
body {
  margin: 0;
}

.wrapper {
  display: flex;
  align-items: center;
  width: 100%;
  height: 100vh;
  background-color: $first-bkg;
}

.container {
  width: 849px;
  padding: 75px 100px;
  margin: 0 auto;

  @include vp-1023 {
    padding: 75px 125px;
  }

  @include vp-767 {
    padding: 75px 46px;
  }
}

.stopwatchs__container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(209px, 225px));
  gap: 45px 50px;
  justify-content: center;

  @include vp-767 {
    grid-template-columns: 1fr;
  }
}
</style>
