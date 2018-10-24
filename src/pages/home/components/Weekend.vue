<template>
    <div>
        <div class="recommend-title">周末去哪儿</div>
        <ul>
            <li class="recommend-item border-bottom" v-for="weekend in weekendList">
                <div class="item-img-wrapper">
                    <img class="item-img" :src="weekend.imgUrl" alt="">
                </div>
                <div class="item-info">
                    <p class="item-title">{{weekend.title}}</p>
                    <p class="item-desc">{{weekend.desc}}</p>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "HomeWeekend",
        props: {
            weekendList: {
                type: Array
            }
        },
        data() {
            return {}
        },
    }
</script>

<style lang="stylus" type="text/stylus" scoped>
    @import "~styles/mixins.styl"

    .recommend-title
        margin-top .2rem
        line-height .8rem
        background #eee
        text-indent .2rem

    .item-img-wrapper
        height 0
        overflow hidden
        padding-bottom 33.9%
        .item-img
            width 100%

    .item-info
        padding .1rem
        min-width 0
        .item-title
            line-height .54rem
            font-size .32rem
            ellipsis()
        .item-desc
            line-height .4rem
            color #ccc
            ellipsis()
</style>