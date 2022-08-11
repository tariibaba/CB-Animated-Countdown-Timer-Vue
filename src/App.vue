<template>
  <AppTimer
    :elapsed="timeElapsed"
    :limit="timeLimit"
  />
</template>

<script>
import AppTimer from './components/AppTimer.vue';

export default {
  name: 'App',
  data() {
    return {
      timeElapsed: 0,
      timerInterval: undefined,
      timeLimit: 10,
    };
  },
  methods: {
    startTimer() {
      this.timerInterval = setInterval(() => {
        // Stop counting when there is no more time left
        if (++this.timeElapsed === this.timeLimit) {
          clearInterval(this.timerInterval);
        }
      }, 1000);
    },
  },
  // Start timer immediately
  mounted() {
    this.startTimer();
  },
  components: {
    AppTimer,
  },
};
</script>
