<template>
  <div>
    <app-stock
      v-for="stock in stockPortfolio"
      :stock="stock"
      :key="stock.id"
    />
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
import Stock from './Stock.vue';

export default {
  computed: {
    ...mapGetters(['stockPortfolio'])
  },
  components: {
    appStock: Stock
  }
}
</script>