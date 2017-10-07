<template>
    <md-layout md-column md-flex>
        <md-layout md-column md-align="center">
            <span class="md-title">
                {{waterBottleCount}} plastic watter bottles have been consumed in the USA.
            </span>
            <span class="md-subheading">
                Each water glass represents {{ valuePerIcon }} plastic bottles.
            </span>
            <a target="_blank" href="http://www.greeneducationfoundation.org/nationalgreenweeksub/waste-reduction-tips/tips-to-use-less-plastic.html">
                Learn to reduce use of plastic items.</a>
        </md-layout>

        <br>

        <md-layout md-align="start">
            <span v-if="waterBottleIconsCount < 1">
                <md-icon md-iconset="fa"></md-icon>
            </span>
            <span v-for="waterBottle in waterBottleIconsCount" :key="waterBottle">
                <md-icon>local_drink</md-icon>
            </span>
            <span v-if="waterBottleIconsCount > 1000" class="md-title">
                + {{ waterBottleIconsCount - 1000 }} more
            </span>
        </md-layout>
    </md-layout>
</template>

<script>
export default {
    computed: {
        waterBottleCount() {
            return Math.floor(this.waterBottle);
        },
        waterBottleIconsCount() {
            return Math.floor(this.waterBottle / this.valuePerIcon);
        }
    },
    created() {
        window.setInterval(() => {
            this.waterBottle += 1500 / 10;
        }, 100);
    },
    data() {
        return {
            waterBottle: 0,
            valuePerIcon: 250
        };
    }
};
</script>

<style scoped>

</style>