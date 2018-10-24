<template>
    <div>
        <home-header></home-header>
        <home-swiper></home-swiper>
        <home-icons></home-icons>
        <home-recommend></home-recommend>
        <home-weekend></home-weekend>
    </div>
</template>

<script>
    import HomeHeader from './components/Header';
    import HomeSwiper from './components/Swiper';
    import HomeIcons from './components/Icons';
    import HomeRecommend from './components/Recommend';
    import HomeWeekend from './components/Weekend';

    export default {
        name: "",
        data() {
            return {
                obj: [{id: 1, name: '测试1'}, {id: 2, name: '测试2'}, {id: 3, name: '测试3'}]
            }
        },
        components: {
            HomeHeader,
            HomeSwiper,
            HomeIcons,
            HomeRecommend,
            HomeWeekend,
        }
    }
</script>

<style scoped>

</style>