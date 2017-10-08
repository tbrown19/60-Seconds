<template>
    <div>
        <md-icon md-iconset="fa fa-heart" class="md-size-3x md-accent"></md-icon>

        <md-layout md-column>
            <md-layout md-align="center">
                <span class="md-display-1">Time since entering site:</span>
            </md-layout>
            <md-layout md-align="center">
                <span class="md-display-3">{{ formatedSeonds }}</span>
            </md-layout>
            <md-layout md-align="center">
                <span class="md-display-1">While you've been here</span>
            </md-layout>
        </md-layout>

        <hr id="seperator">

        <deaths-view :milliSecondsPassed="milliSecondsPassed"></deaths-view>
        <hr class="statistic-seperator">
        <births-view :milliSecondsPassed="milliSecondsPassed"></births-view>
        <hr class="statistic-seperator">
        <garbage-view></garbage-view>
        <hr class="statistic-seperator">
        <water-bottle-use-view></water-bottle-use-view>
        <hr class="statistic-seperator">
        <tree-view></tree-view>
        <hr class="statistic-seperator">
        <oil-view></oil-view>
        <hr class="statistic-seperator">
        <charity-view></charity-view>
        <br>
        <hr id="seperator">
        <span class="md-subheading">
            <em>"For every minute you remain angry, you give up sixty seconds of peace of mind."</em> 
            — Ralph Waldo Emerson
        </span>
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
import BirthsView from './events/Births.vue';
import GarbageView from './events/Garbage.vue';
import WaterBottleUseView from './events/WaterBottleUse.vue';
import TreeView from './events/Trees.vue';
import OilView from './events/Oil.vue';
import CharityView from './events/Charity.vue';
const moment = require('moment');
// require('hacktimer');
export default {
    components: {
        DeathsView, BirthsView, GarbageView, WaterBottleUseView, TreeView, OilView, CharityView
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
        this.startedAt = moment();
        window.setInterval(() => {
            const timePassed = moment() - this.startedAt;
            let secondsPassed = Math.floor(timePassed / 1000);
            this.now = secondsPassed;
            this.milliSecondsPassed = timePassed / 100;
        }, 100);
    },
    data() {
        return {
            startedAt: 0,
            now: 0,
            milliSecondsPassed: 0
        };
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h1,
h2 {
    font-weight: normal;
}

#site-timer {
    font-size: 4rem;
}

#seperator {
    margin: 1rem;
}

.green {
    color: green;
}

.statistic-seperator {
    width: 80%;
    margin-left: auto;
    margin-right: auto;
    margin-top: 1.5rem;
    margin-bottom: 1.5rem;
}

.md-title {
    font-size: 1.4rem;
}

.md-subheading {
    font-size: 1.2rem;
}

a {
    font-size: 1.2rem;
}
</style>
