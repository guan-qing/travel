<template>
    <div class="container" @click="handleGallaryClick">
        <div class="wrapper">
            <swiper :options="swiperOption" v-if="imgs.length>0">
                <swiper-slide v-for="(item,index) in imgs" :key="index">
                    <img class="swiper-img" :src="item" let="">
                </swiper-slide>
                <div class="swiper-pagination" slot="pagination"></div>
            </swiper>
        </div>
    </div>
</template>

<script>
    import {swiper, swiperSlide} from 'vue-awesome-swiper';

    export default {
        name: "",
        props: {
            imgs: {
                type: Array,
                default() {
                    return []
                }
            }
        },
        data() {
            return {
                swiperOption: {
                    pagination: '.swiper-pagination',
                    paginationType: 'fraction',
                    observeParents: true,
                    observer: true
                }
            }
        },
        methods: {
            handleGallaryClick() {
                this.$emit('close');
            }
        },
        components: {
            swiper,
            swiperSlide
        }
    }
</script>

<style scoped lang="stylus" type="text/stylus">
    .swiper-container
        overflow inherit

    .container
        display flex
        flex-direction column
        justify-content center
        position fixed
        left 0
        right 0
        top 0
        bottom 0
        background #000
        z-index 99
        .wrapper
            background #fff
            height 0
            width 100%
            padding-bottom 100%
            .swiper-pagination
                color #fff
                bottom -1rem

    .swiper-img
        width 100%
</style>