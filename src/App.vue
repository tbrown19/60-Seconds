<template>
    <div id="app">
        <md-layout md-gutter>
            <md-layout md-row md-gutter md-align="center">
                  <md-layout md-flex="80" md-align="center">
                    <router-view id="content"/>
                  </md-layout>
            </md-layout>
        </md-layout>
    </div>
</template>

<script>
export default {
    name: 'app'
};
</script>

<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
#content{
    min-width: 100%;
}
</style>
