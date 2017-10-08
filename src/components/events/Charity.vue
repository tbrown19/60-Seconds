<template>
    <md-layout md-column md-flex>
        <md-layout md-column md-align="center">
            <span class="md-title">
                ${{charityCount}} dollars has been donated to charity.
            </span>
            <span class="md-subheading">
                Each $ represents ${{ valuePerIcon }}.
            </span>
            <span class="md-subheading">
                You can help make a difference.
            </span>
            <a href="https://www.charitywatch.org/toprated">Find worthy charities.</a>
        </md-layout>

        <br>

        <md-layout md-align="start">
            <span v-if="charityIconsCount < 1">
                <md-icon md-iconset="fa"></md-icon>
            </span>
            <span v-for="charity in charityIconsCount" :key="charity">
                <md-icon md-iconset="fa fa-usd" class="green-money"></md-icon>
            </span>
            <span v-if="charityIconsCount >= 1000" class="md-title">
                + {{ Math.floor((charityCount - 1000) / this.valuePerIcon) }} more
            </span>
        </md-layout>
    </md-layout>
</template>

<script>
export default {
    computed: {
        charityCount() {
            return Math.floor(this.charity);
        },
        charityIconsCount() {
            if (this.charity / this.valuePerIcon > 1000) {
                return 1000;
            }
            return Math.floor(this.charity / this.valuePerIcon);
        }
    },
    created() {
        window.setInterval(() => {
            this.charity += 52286.45 / 10;
        }, 100);
    },
    data() {
        return {
            charity: 0,
            valuePerIcon: 10000
        };
    }
};
</script>

<style scoped>
.green-money {
    margin-top: 2px;
    color: rgb(0, 177, 106);
}
</style>