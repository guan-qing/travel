<template>
    <div class="wrapper">
        <swiper :options="swiperOption">
            <swiper-slide :key="index" v-for="(swiperImg,index) in swiperList">
                <img class="swiper-img" :src="swiperImg.imgUrl" let="">
            </swiper-slide>
            <div class="swiper-pagination" slot="pagination"></div>
        </swiper>
    </div>
</template>

<script>

    import {swiper, swiperSlide} from 'vue-awesome-swiper';

    export default {
        name: "",
        data() {
            return {
                swiperOption: {
                    loop: true,
                    speed: 1000,
                    autoplay: 3000,
                    pagination: '.swiper-pagination'
                },
                swiperList: [{
                    imgUrl: 'https://imgs.qunarzz.com/vc/d6/f8/02/1f926edfd7e2d040c6063b031b.jpg'
                }, {
                    imgUrl: 'https://imgs.qunarzz.com/ftejia/1808/4a/2c3df86d3fc9ae.jpg'
                }]
            }
        },
        components: {
            swiper,
            swiperSlide
        }
    }
</script>

<style lang="stylus" type="text/stylus" scoped>
    /*scoped 该属性是定义了该css都是私有的,如果要修改到别的样子,则需要用>>>做穿透*/
    .wrapper >>> .swiper-img
        width 100%

    .wrapper
        width 100%
        height 0
        overflow hidden
        padding-bottom 31.25%
        background #ccc
</style>