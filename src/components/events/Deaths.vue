<template>
    <md-layout md-column md-flex>
        <md-layout md-align="center">
            <span class="md-title">
                {{deathsCount}} deaths have occured.
            </span>
        </md-layout>
        <md-layout md-align="start">
            <span v-for="death in deathsArray" :key="death">
                <md-icon v-if="death == 'red'" md-iconset="fa fa-user" class="md-warn"></md-icon>
                <md-icon v-else md-iconset="fa fa-user"></md-icon>
            </span>
        </md-layout>
    </md-layout>
</template>

<script>
export default {
    computed: {
        deathsCount() {
            return Math.floor(this.deaths);
        }
    },
    watch: {
        deaths(newValue, old) {
            const newDeaths = Math.floor(newValue) - Math.floor(old);
            for (let i = 0; i < newDeaths; i++) {
                const color = Math.random() < 0.16 ? 'red' : 'black';
                this.deathsArray.push(color);
            }
            return Math.floor(this.deaths);
        }
    },
    created() {
        window.setInterval(() => {
            this.deaths += 1.783;
        }, 1000);
    },
    data() {
        return {
            deaths: 0,
            deathsArray: []
        };
    }
};
</script>
