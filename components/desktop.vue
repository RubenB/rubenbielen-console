<template>
    <div class="desktop">
        <slot></slot>
    </div>
</template>

<script>
export default {
    
}
</script>

<style lang="scss" scoped>
@import 'assets/scss/global';

.desktop {
    width: 100vw;
    height: 100vh;
    position: relative;
    background-color: lightblue;
}
</style>

