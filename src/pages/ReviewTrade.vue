<template>
  <p>hsddsfdfsi</p>
  <div v-if="trades">
    <p v-for="(trade, id) in trades" :key="id">{{ trade.stock }}</p>
  </div>
  <div v-if="trades">
    <p>{{ trades[0].stock }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'ReviewTradeComponent',
  data() {
    return {
      trades: null,
    };
  },
  methods: {
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
