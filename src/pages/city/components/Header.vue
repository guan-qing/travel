<template>
    <div class="header">
        城市选择
        <router-link to="/">
            <div class="iconfont header-left">&#xe624;</div>
        </router-link>
    </div>
</template>

<script>
    export default {
        name: ""
    }
</script>

<style scoped lang="stylus" type="text/stylus">
    @import "~styles/varibles.styl";
    .header
        overflow hidden
        height $headerHeight
        line-height $headerHeight
        text-align center
        color #fff
        background $bgColor
        font-size .32rem
        position relative
        .header-left
            width .64rem
            text-align center
            position absolute
            top 0
            left 0
            color #fff
</style>