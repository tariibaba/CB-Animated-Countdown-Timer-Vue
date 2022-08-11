<template>
  <div class="background">
    <div
      class="elapsed"
      :style="{ height: '100%', backgroundColor: 'blue' }"
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
      timeLimit: 10,
      timeElapsed: 0,
      timeInterval: undefined,
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
  height: 100%;
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
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}
</style>
