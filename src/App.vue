<template>
  <div class="background">
    <div
      class="elapsed"
      :style="{ height: backgroundHeight, backgroundColor }"
      v-if="timeLeft > 0"
    ></div>
  </div>
  <AppTimer
    :elapsed="timeElapsed"
    :limit="timeLimit"
  />
</template>

<script>
import AppTimer from './components/AppTimer.vue';
export default {
  name: 'App',
  components: { AppTimer },
  data() {
    return {
      timeLimit: 5,
      timeElapsed: 0,
      timeInterval: undefined,
      thresholds: [
        {
          color: 'blue',
          threshold: 1,
        },
        {
          color: 'orange',
          threshold: 0.5,
        },
        {
          color: 'red',
          threshold: 0.2,
        },
      ],
    };
  },
  methods: {
    startTimer() {
      this.timerInterval = setInterval(() => {
        if (++this.timeElapsed === this.timeLimit) {
          clearInterval(this.timerInterval);
        }
      }, 1000);
    },
  },
  computed: {
    timeLeft() {
      return this.timeLimit - this.timeElapsed;
    },
    timeFraction() {
      return this.timeLeft / this.timeLimit;
    },
    backgroundHeight() {
      const timeFraction = this.timeFraction;

      // Adjust time fraction to prevent lag when the time left
      // is 0, like we did for the time left progress ring
      const adjTimeFraction =
        timeFraction - (1 - timeFraction) / this.timeLimit;

      const height = Math.floor(adjTimeFraction * 100);

      return `${height}%`;
    },
    backgroundColor() {
      return this.thresholds.reduce(
        (color, item) =>
          item.threshold >= this.timeFraction ? item.color : color,
        undefined
      );
    },
  },
  mounted() {
    this.startTimer();
  },
};
</script>

<style scoped>
.background {
  height: 100%;
  position: absolute;
  top: 0;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: end;
  background-color: black;
}

.background .elapsed {
  transition: all 1s linear;
}
</style>

<style>
html,
body,
#app {
  height: 100%;
  margin: 0;
}

#app {
  /* Center timer vertically and horizontally */
  display: flex;
  justify-content: center;
  align-items: center;

  position: relative;
}
</style>
