<template>
  <rb-desktop>
    <rb-console></rb-console>
  </rb-desktop>
</template>

<script>
import rbConsole from '@/components/console';
import rbDesktop from '@/components/desktop';

export default {
  components: {
    rbConsole,
    rbDesktop
  }
}
</script>

<style lang="scss">
@import "assets/scss/global";
</style>

