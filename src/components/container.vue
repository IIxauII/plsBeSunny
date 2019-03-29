<template lang="pug">
    div.container
        <weatherApp/>
</template>
<script>
import weatherApp from './weather';

export default {
    name: 'container',
    components: {
        weatherApp,
    },
    data() {
        return {
            msg: 'this is a container',
        };
    },
};
</script>
<style lang="scss">
    .container {
        display: flex;
        height: 50%;
        width: 50%;
        margin: auto;
        background-color: rgba(20, 20, 20, 0.5);
        box-shadow: 0px 0px 28px 12px rgba(0,0,0,0.5);
        border-radius: 15px;
    }
</style>
