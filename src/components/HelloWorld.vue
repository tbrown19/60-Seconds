<template>
    <div class="hello">
        <h2>Time since entering site</h2>
        <span id="site-timer">{{ formatedSeonds }}</span>
        <br>
        <md-button class="md-raised md-primary">Button</md-button>
        <div style="text-align:left;">
            <span v-for="death in deathsCount" :key="death">
                {{ death }}
            </span>
        </div>
    </div>
</template>

<script>
const moment = require('moment');
export default {
    computed: {
        formatedSeonds() {
            return moment.utc(this.now * 1000).format('HH:mm:ss');
        },
        deathsCount() {
            return Math.floor(this.deaths);
        }
    },
    created() {
        window.setInterval(() => {
            this.now += 1;
        }, 1000);
        window.setInterval(() => {
            this.deaths += 1.783;
        }, 1000);
    },
    data() {
        return {
            now: 0,
            deaths: 0
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

#site-timer {
    font-size: 4rem;
}
</style>
