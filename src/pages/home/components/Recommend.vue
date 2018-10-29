<template>
    <div>
        <div class="recommend-title">热门推荐</div>
        <ul>
            <router-link :key="recommend.id" tag="li" :to="'/detail/'+recommend.id" class="recommend-item border-bottom"
                         v-for="recommend in recommendList">
                <div class="item-img-wrapper">
                    <img class="item-img" :src="recommend.imgUrl" alt="">
                </div>
                <div class="item-info">
                    <p class="item-title">{{recommend.title}}</p>
                    <p class="item-desc">{{recommend.desc}}</p>
                    <button class="item-button">查看详情</button>
                </div>
            </router-link>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "HomeRecommend",
        props: {
            recommendList: {
                type: Array
            }
        },
        data() {
            return {}
        }
    }
</script>

<style lang="stylus" type="text/stylus" scoped>
    @import "~styles/mixins.styl"

    .recommend-title
        margin-top .2rem
        line-height .8rem
        background #eee
        text-indent .2rem

    .recommend-item
        display flex
        height 1.9rem
        overflow hidden
        .item-img
            width 1.7rem
            height 1.7rem
            padding .1rem
        .item-info
            flex 1
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
            .item-button
                color #fff
                line-height .44rem
                margin-top .2rem
                background #ff9300
                padding 0 .2rem
                border-radius .06rem
</style>