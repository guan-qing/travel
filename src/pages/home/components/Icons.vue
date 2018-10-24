<template>
    <div class="icons">
        <swiper :options="swiperOption" v-if="iconList&&iconList.length">
            <swiper-slide :key="index" v-for="(items,index) in pages">
                <div class="icon" v-for="icon in items">
                    <div class="icon-img">
                        <img class="icon-img-content" :src="icon.imgUrl" alt="">
                        <p class="icon-desc">{{icon.desc}}</p>
                    </div>
                </div>
            </swiper-slide>
            <div class="swiper-pagination" slot="pagination"></div>
        </swiper>
    </div>
</template>

<script>
    import {swiper, swiperSlide} from 'vue-awesome-swiper';

    export default {
        name: "HomeIcons",
        props: {
            iconList: {
                type: Array
            }
        },
        data() {
            return {
                swiperOption: {},
            }
        },
        computed: {
            pages() {
                let pages = [];
                this.iconList.forEach((item, index) => {
                    const page = Math.floor(index / 8);
                    if (!pages[page]) {
                        pages[page] = [];
                    }
                    pages[page].push(item);
                });
                return pages;
            }
        },
        components: {
            swiper,
            swiperSlide
        }
    }
</script>

<style scoped lang="stylus" type="text/stylus">
    @import "~styles/varibles.styl";
    @import "~styles/mixins.styl";
    .icons >>> .swiper-container
        height 0
        padding-bottom 50%

    .icon
        height 0
        width 25%
        float left
        padding-bottom 25%
        position relative
        text-align center
        overflow hidden
        .icon-img
            position absolute
            top 0
            left 0
            right 0
            bottom .44rem
            padding .3rem
            height 100%
            box-sizing border-box
            .icon-img-content
                height 100%
                display block
                margin 0 auto
        .icon-desc
            position absolute
            left 0
            right 0
            bottom 0
            height .44rem
            line-height .64rem
            text-align center
            color $darkTextColor
            ellipsis()

</style>