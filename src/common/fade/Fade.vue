<template>
    <transition name="">
        <slot></slot>
    </transition>

</template>

<script>
    export default {
        name: "Fade",
    }
</script>

<style scoped lang="stylus" type="text/stylus">
    .v-enter, .v-leave-to
        opacity 0

    .v-enter-active, .v-leave-active
        transition opacity 0.5s
</style>