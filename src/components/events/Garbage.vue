<template>
    <md-layout md-column md-flex>
        <md-layout md-column md-align="center">
            <span class="md-title">
                {{tonsTrashCount}} tons of garbage has been generated.
            </span>
            <span class="md-subheading">
                Each trashcan represents 100 tons.
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
                <md-icon md-iconset="fa fa-trash"></md-icon>
            </span>
            <span v-if="tonsTrashIconsCount > 1000" class="md-title">
                + {{ tonsTrashIconsCount - 1000 }} more
            </span>
        </md-layout>
    </md-layout>
</template>

<script>
export default {
    computed: {
        tonsTrashCount() {
            return Math.floor(this.tonsTrash);
        },
        tonsTrashIconsCount() {
            return Math.floor(this.tonsTrash / this.valuePerIcon);
        }
    },
    created() {
        window.setInterval(() => {
            this.tonsTrash += 41.667 / 10;
        }, 100);
    },
    data() {
        return {
            tonsTrash: 0,
            valuePerIcon: 100
        };
    }
};
</script>

<style scoped>

</style>