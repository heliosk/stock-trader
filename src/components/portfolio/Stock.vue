<template>
  <div class="col-sm-6 col-md-4">
    <div class="panel panel-info">
      <div class="panel-heading">
        <h3 class="panel-title">
          {{ stock.name }}
          <small>(Price: {{ stock.price }} | Quantity: {{ stock.quantity }})</small>
        </h3>
      </div>
    </div>
    <div class="panel-body">
      <div class="pull-left">
        <input
          type="number"
          class="form-control"
          placeholder="Quantity"
          v-model="quantity"
          :class="{danger: insufficientQuantity}"
        >
      </div>
      <div class="pull-right">
        <button
          class="btn btn-success"
          @click="sellStock"
          :disabled="insufficientQuantity || quantity <= 0"
        >
          {{ insufficientQuantity ? 'Not enough stocks' : 'Sell' }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex';

export default {
  name: 'Stock',
  props: {
    stock: {
      type: Object,
      default: null
    }
  },
  data() {
    return {
      quantity: 0
    }
  },
  computed: {
    insufficientQuantity() {
      return this.quantity > this.stock.quantity;
    }
  },
  methods: {
      ...mapActions({
        placeSellOrder: 'sellStock'
      }),
      sellStock() {
        const order = {
          stockId: this.stock.id,
          quantity: Number(this.quantity),
          stockPrice: this.stock.price
        };
        this.placeSellOrder(order);
        this.quantity = 0;
      }
  }
};
</script>

<style scoped>
.danger {
  border: 1px solid red;
}
</style>
