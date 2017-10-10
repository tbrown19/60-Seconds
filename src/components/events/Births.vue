<template>
    <md-layout md-column md-flex>
        <md-layout md-column md-align="center">
            <span class="md-title">
                {{birthsCount}} children have been born.
            </span>
            <span class="md-title md-warn">
                <span class="orange"> {{povertyBirthsCount}} </span> were born into poverty.
            </span>
            <span class="md-subheading">
                Orange represents a child born into poverty.
            </span>
            <a target="_blank" href="http://endpoverty.org/">Help end poverty.</a>
        </md-layout>

        <br>

        <md-layout md-align="start">
            <span v-for="birth in birthsArray" :key="birth">
                <md-icon v-if="birth == 'red'" md-iconset="fa fa-user" class="orange-person"></md-icon>
                <md-icon v-else md-iconset="fa fa-user"></md-icon>
            </span>
            <span v-if="births > 1000" class="md-title">
                + {{ birthsCount - 1000 }} more
            </span>
        </md-layout>
    </md-layout>
</template>

<script>
export default {
    props: ['milliSecondsPassed'],
    computed: {
        birthsCount() {
            return Math.floor(this.births);
        },
        povertyBirthsCount() {
            return Math.floor(this.povertyBirths);
        }
    },
    watch: {
        births(newValue, old) {
            // only display up to 1000 items,
            if (newValue < 1000) {
                const newBirths = Math.floor(newValue) - Math.floor(old);
                for (let i = 0; i < newBirths; i++) {
                    const color = Math.random() < 0.52 ? 'red' : 'black';
                    this.birthsArray.push(color);
                }
            }
        }
    },
    created() {
        window.setInterval(() => {
            this.births = 0.0416 * this.milliSecondsPassed;
            this.povertyBirths = 0.0188 * this.milliSecondsPassed;
        }, 100);
    },
    data() {
        return {
            births: 0,
            povertyBirths: 0,
            birthsArray: []
        };
    }
};
</script>

<style scoped>
.orange-person {
    color: rgb(249, 105, 14);
}
</style>