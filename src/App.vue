<template lang="pug">
    div#app
        container
</template>

<script>
import container from './components/container';

export default {
    name: 'App',
    components: {
        container,
    },
};
</script>

<style lang="scss">
    html {
        font-size: 16px;
    }
    body {
        margin: 0;
        padding: 0;
    }
    #app {
        display: flex;
        height: 100vh;
        width: 100vw;
        margin: 0;
        padding: 0;
        background: url('https://xaucpw.ddnss.de/media/images/feelslonelyroadwallpaper.jpg');
    }
</style>

