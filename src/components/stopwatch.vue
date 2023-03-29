<template>
  <div class="stopwatch">
    <div class="stopwatch__time">
      <div class="hours" :style="{ color: !isRunning ? '#ffffff' : '#9E9E9E' }" v-if="hoursVisible">
        {{ hrs + ':' }}
      </div>
      <div class="minutes" :style="{ color: !isRunning ? '#ffffff' : '#9E9E9E' }" v-if="minutesVisible">
        {{ min + ':' }}
      </div>
      <div class="seconds" :style="{ color: !isRunning ? '#ffffff' : '#9E9E9E' }">
        {{ sec }}
      </div>
    </div>
    <div class="stopwatch__control-buttons">
      <button class="button" @click="clickStart">
        <img :src="playImg" alt="Запустить" />
        <span class="visually-hidden">включить</span>
      </button>

      <button class="button button--stop" @click="clickStop" :style="{ background: isRunning ? '#9e9e9e' : '#ffffff' }">
        <span class="visually-hidden">стоп</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'stopwatch',
  data() {
    return {
      sec: `0${0}`,
      min: `0${0}`,
      hrs: `0${0}`,

      playImg: 'src/assets/images/iconPlay.svg',
      pauseImg: 'src/assets/images/iconPause.svg',
      // stopImg: 'src/assets/images/iconStop.svg',

      interval: null,
      visible: false,
      hoursVisible: false,
      minutesVisible: false,
      isRunning: true,
    };
  },
  methods: {
    clickStart() {
      if (this.isRunning) {
        this.playImg = !this.isRunning ? this.pauseImg : 'src/assets/images/iconPause.svg';
        this.interval = setInterval(() => {
          this.sec++;
          this.sec < 10 ? (this.sec = `0${this.sec}`) : this.sec;
          if (this.sec >= 60) {
            this.sec = `0${0}`;
            this.minutesVisible = true;
            this.min++;
            this.min < 10 ? (this.min = `0${this.min}`) : this.min;
            if (this.min >= 60) {
              this.min = `0${0}`;
              this.hoursVisible = true;
              this.hrs++;
            }
          }
        }, 1000);
      } else {
        clearInterval(this.interval);
        this.pauseImg = this.playImg;
      }
      this.playImg = this.isRunning ? 'src/assets/images/iconPause.svg' : 'src/assets/images/iconPlay.svg';
      this.isRunning = !this.isRunning;
    },
    clickStop() {
      clearInterval(this.interval);
      this.sec = `0${0}`;
      this.min = 0;
      this.hrs = 0;
      this.isRunning = true;
      this.playImg = !this.isRunning ? this.playImg : 'src/assets/images/iconPlay.svg';
    },
  },
  computed: {
    buttonLabel() {
      return this.isRunning ? 'Stop' : 'Start';
    },
  },
};
</script>

<style lang="scss">
.stopwatch {
  position: relative;
  min-height: 120px;
  background-color: $stopwath-bkg;

  display: flex;
  flex-direction: column;
  justify-content: space-between;

  font-size: 22px;
  line-height: 21px;
  color: $off-stopwath-color;

  &::after {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    width: 100%;
    height: 1px;
    transform: translate(-50%, -50%);
    border-bottom: 1px solid #9e9e9e;
  }
}

.stopwatch__time {
  display: flex;
  justify-content: center;
  padding: 22px 0;
}

.stopwatch__control-buttons {
  display: grid;
  grid-template-columns: repeat(2, 20px);
  column-gap: 48px;
  justify-content: center;
  padding: 22px 0;
}

.button {
  background: transparent;
  display: block;
  padding: 0;
  border: none;

  width: 20px;
  height: 20px;

  &--stop {
    background-color: #9e9e9e;
  }

  &:focus {
    outline: 1px solid $off-stopwath-color;
    outline-offset: 3px;
  }
}

.seconds,
.minutes,
.hours {
  transition: color 0.5s;
}

.seconds,
.minutes,
.hours.start {
  color: #ffffff;
}

.seconds,
.minutes,
.hours.stop {
  color: #9e9e9e;
}
</style>
