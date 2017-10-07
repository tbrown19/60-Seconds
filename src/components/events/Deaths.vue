<template>
    <md-layout md-column md-flex>
        <md-layout md-column md-align="center">
            <span class="md-title">
                {{deathsCount}} deaths have occured.
            </span>
            <span class="md-title md-warn">
                <span class="orange"> {{starvationDeathsCount}} </span>because of starvation.
            </span>
            <span class="md-subheading">
                Orange represents a death due to starvation.
            </span>
            <a target="_blank" href="https://www.riseagainsthunger.org/">Help end world hunger.</a>
        </md-layout>

        <br>

        <md-layout md-align="start">
                <span v-for="death in deathsArray" :key="death">
                    <md-icon v-if="death == 'red'" md-iconset="fa fa-user" class="md-warn"></md-icon>
                    <md-icon v-else md-iconset="fa fa-user"></md-icon>
                </span>
            <span v-if="deaths > 1000" class="md-title">
                + {{ deathsCount - 1000 }} more
            </span>
        </md-layout>
    </md-layout>
</template>

<script>
export default {
    computed: {
        deathsCount() {
            return Math.floor(this.deaths);
        },
        starvationDeathsCount() {
            return Math.floor(this.starvationDeaths);
        }
    },
    watch: {
        deaths(newValue, old) {
            // only display up to 1000 items,
            if (newValue < 1000) {
                const newDeaths = Math.floor(newValue) - Math.floor(old);
                for (let i = 0; i < newDeaths; i++) {
                    const color = Math.random() < 0.16 ? 'red' : 'black';
                    this.deathsArray.push(color);
                }
            }
        }
    },
    created() {
        window.setInterval(() => {
            this.deaths += 1.783 / 10;
            this.starvationDeaths += 0.3 / 10;
        }, 100);
    },
    data() {
        return {
            deaths: 0,
            starvationDeaths: 0,
            deathsArray: []
        };
    }
};
</script>

<style scoped>
</style>