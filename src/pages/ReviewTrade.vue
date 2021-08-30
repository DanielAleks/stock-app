<template>
  <div class="review-section">
    <h3>Review Your trades</h3>
    <p>Today: January 1st, 2021</p>
    <div class="review-card" v-for="(trade, id) in trades" :key="id">
      <q-card class="my-card card-styles">
        <q-card-section class="text-white row justify-center">
          <p>{{ trade.stock }}</p>
          <p class="q-mx-sm">{{ trade.execution }}</p>
          <p>{{ trade.pattern }}</p>
        </q-card-section>

        <q-separator />

        <q-card-actions align="right" class="column">
          <p>Investment: {{ trade.bought * trade.shares }}</p>
          <p>Gain/Loss: {{ trade.bought - trade.sold * trade.shares }}</p>
          <p>Difference: {{ trade.bought }}$ - {{ trade.sold }}$</p>
        </q-card-actions>
      </q-card>
    </div>
  </div>
</template>

<style lang="scss">
.review-section {
  display: flex; 
  flex-direction: column;
  align-items: center;
}
.card-styles {
  width: 20rem;
  background: rgba(128, 128, 128, 0.521);
  backdrop-filter: blur(5px);
}
</style>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'ReviewTradeComponent',
  data() {
    return {
      trades: {},
    };
  },
  methods: {
    // coolBeans ({trade})   {
    //   const fire = trade.bought - trade.sold
    //   fire * trade.shares
    // },
    fetchData: async function () {
      const response = await fetch('http://localhost:3000/api');
      const data = await response.json();
      this.trades = data;
      console.log(data, 'me');
    },
  },
  created() {
    this.fetchData();
  },
});
</script>
