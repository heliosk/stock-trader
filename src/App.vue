<template>
  <div id="app">
    <app-header />
    <div class="row">
      <div class="col-md-12">
        <router-view />
      </div>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue';

export default {
  name: 'App',
  components: {
    appHeader: Header,
  },
  created() {
    this.$store.dispatch('initStocks');
  }
};
</script>

<style>
body {
  padding: 30px;
}
</style>
