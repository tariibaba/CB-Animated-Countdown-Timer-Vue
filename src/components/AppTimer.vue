<template>
  <div class="root">
    <svg class="svg" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
      <g class="circle">
        <circle class="time-elapsed-path" cx="50" cy="50" r="45" />
      </g>
    </svg>
  </div>
</template>

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
</style>
