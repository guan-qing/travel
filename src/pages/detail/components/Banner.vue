<template>
    <div>
        <div class="banner" @click="showGallary=true">
            <img class="banner-img"
                 src="http://img1.qunarzz.com/sight/p0/1810/2d/2d7b45e94187416ea3.img.jpg_600x330_26145653.jpg"
                 alt="">
            <div class="banner-info">
                <div class="banner-title">长隆野生动物世界(AAAAA景区)</div>
                <div class="banner-number"><span class="iconfont">&#xe67f;</span>103</div>
            </div>
        </div>
        <gallary @close="showGallary=false" :imgs="imgs" v-show="showGallary"></gallary>
    </div>
</template>

<script>
    import Gallary from 'common/gallary/Gallary'

    export default {
        name: "",
        data() {
            return {
                imgs: ['http://img1.qunarzz.com/sight/p0/1810/2d/2d7b45e94187416ea3.img.jpg_r_800x800_39d8c7f2.jpg','http://img1.qunarzz.com/sight/p0/1709/41/411f234d79457081a3.img.jpg_r_800x800_ea3a0585.jpg'],
                showGallary: false
            }
        },
        components: {
            Gallary
        }
    }
</script>

<style scoped lang="stylus" type="text/stylus">
    .banner
        overflow: hidden
        height 0
        padding-bottom 55%
        position relative
        .banner-img
            width 100%
        .banner-info
            position absolute
            display flex
            color #fff
            left 0
            right 0
            bottom 0
            line-height .6rem
            background-image linear-gradient(top, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.8))
            .banner-title
                flex 1
                font-size .32rem
                padding 0 .2rem
            .banner-number
                height .32rem
                padding 0 .4rem
                line-height .32rem
                font-size .24rem
                border-radius .2rem
                margin-top .14rem
                background rgba(0, 0, 0, .8)
                .iconfont
                    font-size 10px
</style>