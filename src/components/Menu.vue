<template>
    <div class="menu">
        <a v-for="a in menu" :key="a">{{ a }}</a>
    </div>  
</template>

<script>
export default {
    name: 'TopMenu',
    props: {
        menu: Array,
    }
}
</script>

<style>

</style>