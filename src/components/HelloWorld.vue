<template>
    <div>
        <md-icon md-iconset="fa fa-heart" class="md-size-3x md-accent"></md-icon>

        <md-layout md-column>
            <md-layout md-align="center">
                <span class="md-display-2">Time since entering site</span>
            </md-layout>
            <md-layout md-align="center">
                <span class="md-display-4">{{ formatedSeonds }}</span>
            </md-layout>
            <md-layout md-align="center">
                <span class="md-display-2">While you've been here:</span>
            </md-layout>
        </md-layout>

        <hr id="seperator">
        
        <deaths-view></deaths-view>

        <!-- <md-layout md-column md-flex>
            <md-layout md-align="center">
                <span class="md-title">
                    {{birthsCount}} births have occured.
                </span>
            </md-layout>
            <md-layout md-align="start">
                <span v-for="birth in birthsCount" :key="birth">
                    <md-icon md-iconset="fa fa-user-o" class="green"></md-icon>
                </span>
            </md-layout>
        </md-layout> -->

    </div>
</template>

<script>
import DeathsView from './events/Deaths.vue';
const moment = require('moment');
export default {
    components: {
        DeathsView
    },
    computed: {
        formatedSeonds() {
            return moment.utc(this.now * 1000).format('HH:mm:ss');
        },
        birthsCount() {
            return Math.floor(this.births);
        }
    },
    created() {
        window.setInterval(() => {
            this.now += 1;
        }, 1000);
        window.setInterval(() => {
            this.births += 4.16;
        }, 1000);
    },
    data() {
        return {
            now: 0,
            births: 0
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
#seperator{
    margin: 1rem;
}
.green{
    color: green;
}
</style>
