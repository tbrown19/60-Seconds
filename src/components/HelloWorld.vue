<template>
    <div class="hello">
        <h2>Time since entering site</h2>
        <span id="site-timer">{{ formatedSeonds }}</span>
        <br>
    </div>
</template>

<script>
const moment = require('moment');
export default {
    computed: {
        formatedSeonds() {
            return moment.utc(this.now * 1000).format('HH:mm:ss');
        }
    },
    created() {
        window.setInterval(() => {
            this.now += 1;
        }, 10);
    },
    data() {
        return {
            now: 0
        };
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
    font-weight: normal;
}

#site-timer{
    font-size: 4rem;
}
</style>
