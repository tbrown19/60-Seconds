<template>
    <md-layout md-column md-flex>
        <md-layout md-column md-align="center">
            <span class="md-title">
                {{tonsTrashCount}} tons of garbage have been dumped.
            </span>
            <span class="md-subheading">
                Each trashcan represents {{ valuePerIcon }} tons.
            </span>
            <a target="_blank" href="https://www.epa.gov/recycle/reducing-waste-what-you-can-do/">
                Learn to reduce waste.</a>
        </md-layout>

        <br>

        <md-layout md-align="start">
            <span v-if="tonsTrashIconsCount < 1">
                <md-icon md-iconset="fa"></md-icon>
            </span>
            <span v-for="ton in tonsTrashIconsCount" :key="ton">
                <md-icon v-if="ton < 1000" md-iconset="fa fa-trash"></md-icon>
            </span>
            <span v-if="tonsTrashIconsCount >= 1000" class="md-title">
                + {{ Math.floor((tonsTrashCount - 1000) / this.valuePerIcon) }} more
            </span>
        </md-layout>
    </md-layout>
</template>

<script>
export default {
    props: ['milliSecondsPassed'],
    computed: {
        tonsTrashCount() {
            return Math.floor(this.tonsTrash);
        },
        tonsTrashIconsCount() {
            if (this.tonsTrash / this.valuePerIcon > 1000) {
                return 1000;
            }
            return Math.floor(this.tonsTrash / this.valuePerIcon);
        }
    },
    created() {
        window.setInterval(() => {
            this.tonsTrash = 0.41667 * this.milliSecondsPassed;
        }, 100);
    },
    data() {
        return {
            tonsTrash: 0,
            valuePerIcon: 10
        };
    }
};
</script>

<style scoped>

</style>