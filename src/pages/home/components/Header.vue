<template>
    <div class="header">
        <div class="header-left">
            <div class="iconfont">&#xe624;</div>
        </div>
        <div class="header-input"><span class="iconfont">&#xe632;</span> 输入城市/景点/游玩主题</div>
        <div class="header-right">城市<span class="iconfont">&#xeb6d;</span></div>
    </div>
</template>

<script>
    export default {
        name: "Header"
    }
</script>

<style lang="stylus" type="text/stylus" scoped>
    @import "~styles/varibles.styl";

    .header
        display flex
        background $bgColor
        height $headerHeight
        line-height $headerHeight
        color #fff
        .header-left
            width .64rem
            float left
            text-align center
        .header-input
            height .64rem
            flex 1
            margin-top .12rem
            margin-left .2rem
            background #fff
            border-radius .1rem
            color #ccc
            line-height .64rem
            padding-left .2rem
            .iconfont
                vertical-align top
        .header-right
            width 1.24rem
            float right
            text-align center
            .iconfont
                font-size .24rem
                vertical-align top

</style>