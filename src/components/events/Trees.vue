<template>
    <md-layout md-column md-flex>
        <md-layout md-column md-align="center">
            <span class="md-title">
                {{treeCount}} trees were cut down.
            </span>
            <span class="md-subheading">
                Each tree represents {{ valuePerIcon }} trees cut down.
            </span>
            <a target="_blank" href="http://www.greenpeace.org/usa/forests/solutions-to-deforestation/">
                Learn about deforestation.</a>
        </md-layout>

        <br>

        <md-layout md-align="start">
            <span v-if="treeIconsCount < 1">
                <md-icon md-iconset="fa"></md-icon>
            </span>
            <span v-for="tree in treeIconsCount" :key="tree">
                <md-icon md-iconset="fa fa-tree" class="green-tree"></md-icon>
            </span>
            <span v-if="treeIconsCount >= 1000" class="md-title">
                + {{ Math.floor((treeCount - 1000) / this.valuePerIcon) }} more
            </span>
        </md-layout>
    </md-layout>
</template>

<script>
export default {
    props: ['milliSecondsPassed'],
    computed: {
        treeCount() {
            return Math.floor(this.tree);
        },
        treeIconsCount() {
            if (this.tree / this.valuePerIcon > 1000) {
                return 1000;
            }
            return Math.floor(this.tree / this.valuePerIcon);
        }
    },
    created() {
        window.setInterval(() => {
            this.tree = 0.34 * this.milliSecondsPassed;
        }, 100);
    },
    data() {
        return {
            tree: 0,
            valuePerIcon: 10
        };
    }
};
</script>

<style scoped>
    .green-tree{
        margin-top: 2px;
        color: rgb(39, 174, 96);
    }
</style>