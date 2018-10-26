<template>
    <div>
        <home-header></home-header>
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
    import {mapState} from 'vuex';

    export default {
        name: "",
        data() {
            return {
                lastCity: '',
                homes: {},
            }
        },
        created() {
            this.getHomeInfo();
            this.lastCity = this.city;
        },
        computed: {
            ...mapState(['city'])
        },
        methods: {
            getHomeInfo() {
                axios.get('/api/index.json?city=' + this.city).then((res) => {
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
        },
        activated() {//路由缓存会触发这个生命周期钩子
            if (this.lastCity !== this.city) {
                this.lastCity = this.city;
                this.getHomeInfo();
            }
        }
    }
</script>

<style scoped>

</style>