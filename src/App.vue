<template>
  <AppTimer :elapsed="0" :limit="10" />
</template>

<script>
import AppTimer from './components/AppTimer.vue';

export default {
  name: 'App',
  components: {
    AppTimer,
  },
};
</script>
