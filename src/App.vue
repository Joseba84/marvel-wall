<template>
  <div id="app">
    <search></search>
    <grid></grid>
  </div>
</template>

<script>
import Grid from './components/Grid';
import Search from './components/Search';

export default {
  name: 'app',
  components: {
    Grid,
    Search,
  },
};
</script>

<style lang="scss">
 @import 'main.scss';
</style>
