<template>
    <md-layout md-column md-flex>
        <md-layout md-column md-align="center">
            <span class="md-title">
                {{oilCount}} barrels of oil were used.
            </span>
            <span class="md-subheading">
                Each droplet represents {{ valuePerIcon }} barrels of oil.
            </span>
            <a target="_blank" href="https://www.nrel.gov/workingwithus/learning.html">
                Learn about renewable energy alternatives.</a>
        </md-layout>

        <br>

        <md-layout md-align="start">
            <span v-if="oilIconsCount < 1">
                <md-icon md-iconset="fa"></md-icon>
            </span>
            <span v-for="oil in oilIconsCount" :key="oil">
                <md-icon md-iconset="fa fa-tint" class="black-oil"></md-icon>
            </span>
            <span v-if="oilIconsCount >= 1000" class="md-title">
                + {{ Math.floor((oilCount - 1000) / this.valuePerIcon) }} more
            </span>
        </md-layout>
    </md-layout>
</template>

<script>
export default {
    props: ['milliSecondsPassed'],
    computed: {
        oilCount() {
            return Math.floor(this.oil);
        },
        oilIconsCount() {
            if (this.oil / this.valuePerIcon > 1000) {
                return 10;
            }
            return Math.floor(this.oil / this.valuePerIcon);
        }
    },
    created() {
        window.setInterval(() => {
            this.oil = 9.166 * this.milliSecondsPassed;
        }, 100);
    },
    data() {
        return {
            oil: 0,
            valuePerIcon: 250
        };
    }
};
</script>

<style scoped>
</style>