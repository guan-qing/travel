<template>
    <div>
        <Header></Header>
        <HomeSwiper></HomeSwiper>
        <HomeIcons></HomeIcons>
    </div>
</template>

<script>
    import Header from './components/Header';
    import HomeSwiper from './components/Swiper';
    import HomeIcons from './components/Icons';

    export default {
        name: "",
        components: {
            Header,
            HomeSwiper,
            HomeIcons
        }
    }
</script>

<style scoped>

</style>