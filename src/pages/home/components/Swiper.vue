<template>
    <div class="wrapper">
        <swiper :options="swiperOption" v-if="swiperList&&swiperList.length">
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
        props: {
            swiperList: {
                type: Array,
            }
        },
        data() {
            return {
                swiperOption: {
                    loop: true,
                    speed: 1000,
                    autoplay: 3000,
                    pagination: '.swiper-pagination'
                }
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
    .wrapper >>> .swiper-pagination-bullet-active
        background #fff !important

    .wrapper >>> .swiper-img
        width 100%

    .wrapper
        width 100%
        height 0
        overflow hidden
        padding-bottom 31.25%
        background #ccc
</style>