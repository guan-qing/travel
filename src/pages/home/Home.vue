<template>
    <div>
        <home-header :city="homes.city"></home-header>
        <home-swiper :swiperList="homes.swiperList"></home-swiper>
        <home-icons :iconList="homes.iconList"></home-icons>
        <home-recommend :recommendList="homes.recommendList"></home-recommend>
        <home-weekend :weekendList="homes.weekendList"></home-weekend>
    </div>
</template>

<script>
    import HomeHeader from './components/Header';
    import HomeSwiper from './components/Swiper';
    import HomeIcons from './components/Icons';
    import HomeRecommend from './components/Recommend';
    import HomeWeekend from './components/Weekend';
    import axios from 'axios';

    export default {
        name: "",
        data() {
            return {
                city: '',
                homes: {},
            }
        },
        created() {
            this.getHomeInfo();
        },
        methods: {
            getHomeInfo() {
                axios.get('/api/index.json').then((res) => {
                    if (res.data.ret) this.homes = res.data.data;
                });
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