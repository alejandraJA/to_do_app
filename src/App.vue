<template>
<section>
    <ButtonAdd name="Add" />
    <button>hola</button>
</section>
</template>

<script>
import ButtonAdd from './components/ButtonAdd.vue';
export default {
    name: 'App',
    components: {
        ButtonAdd
    }
}
</script>

<style scoped>
#app {
    width: 98%;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin: 1% 1% 1% 1%;
}
</style>
