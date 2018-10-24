<template>
    <div class="city">
        <city-header></city-header>
        <city-search></city-search>
    </div>
</template>

<script>
    import CityHeader from './components/Header'
    import CitySearch from './components/Search'

    export default {
        name: "",
        components: {
            CityHeader,
            CitySearch
        }
    }
</script>

<style scoped lang="stylus" type="text/stylus">

</style>