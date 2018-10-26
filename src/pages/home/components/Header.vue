<template>
    <div class="header">
        <div class="header-left">
            <div class="iconfont">&#xe624;</div>
        </div>
        <div class="header-input"><span class="iconfont">&#xe632;</span> 输入城市/景点/游玩主题</div>
        <router-link to="/city">
            <div class="header-right">{{city}}<span class="iconfont">&#xeb6d;</span></div>
        </router-link>
    </div>
</template>

<script>
    import {mapState} from 'vuex';

    export default {
        name: "Header",
        computed: {
            ...mapState(['city'])
        }
    }
</script>

<style lang="stylus" type="text/stylus" scoped>
    @import "~styles/varibles.styl";
    @import "~styles/mixins.styl";
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
            color #fff
            ellipsis()
            .iconfont
                font-size .24rem
                vertical-align top

</style>