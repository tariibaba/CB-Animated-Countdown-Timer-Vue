<template>
  <div class="root">
    <svg class="svg" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
      <g class="circle">
        <circle class="time-elapsed-path" cx="50" cy="50" r="45" />
      </g>
    </svg>
    <div class="time-left-container">
      <span class="time-left-label">{{ timeLeftString }}</span>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    padToTwo(num) {
      return String(num).padStart(2, '0');
    },
  },
  computed: {
    timeLeftString() {
      const timeLeft = this.timeLeft;
      const minutes = Math.floor(timeLeft / 60);
      const seconds = timeLeft % 60;
      return `${this.padToTwo(minutes)}:${this.padToTwo(seconds)}`;
    },
    timeLeft() {
      return this.limit - this.elapsed;
    },
  },
  props: {
    elapsed: {
      type: Number,
      required: true,
    },
    limit: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style>
/** Sets the container's height and width */
.root {
  height: 300px;
  width: 300px;
  position: relative;
}

/** Removes SVG styling that would hide the time label */
.circle {
  fill: none;
  stroke: none;
}

/** The SVG path that displays the timer's progress */
.time-elapsed-path {
  stroke-width: 7px;
  stroke: #424242;
}

.time-left-container {
  /** Size should be the same as that of parent container */
  height: inherit;
  width: inherit;

  /** Place container on top of circle ring */
  position: absolute;
  top: 0;

  /** Center content (label) vertically and horizontally  */
  display: flex;
  align-items: center;
  justify-content: center;
}

.time-left-label {
  font-size: 70px;
  font-family: 'Segoe UI';
  color: black;
}
</style>
