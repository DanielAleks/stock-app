<template>
  <div class="q-pa-md bg-image">
    <div
      class="q-gutter-y-md row q-my-sm items-center"
      style="max-width: 500px"
    >
      <p class="text-h5 q-mr-xl">Stock:</p>
      <q-input bg-color="white" filled v-model="stockValue" />
    </div>
    <div
      class="q-gutter-y-md row q-my-sm items-center"
      style="max-width: 500px"
    >
      <p class="text-h5 q-mr-xl">Shares:</p>
      <q-input bg-color="white" filled v-model="shares" />
    </div>
    <div
      class="q-gutter-y-md row q-my-sm items-center"
      style="max-width: 500px"
    >
      <p class="text-h5 q-mr-xl">Bought:</p>
      <q-input bg-color="white" filled v-model="bought" />
    </div>
    <div
      class="q-gutter-y-md row q-my-sm items-center"
      style="max-width: 500px"
    >
      <p class="text-h5 q-mr-xl">Sold:</p>
      <q-input bg-color="white" filled v-model="sold" />
    </div>
    <div
      class="q-gutter-y-md row q-my-sm items-center"
      style="max-width: 500px"
    >
      <p class="text-h5 q-mr-xl">Pattern:</p>
      <q-input bg-color="white" filled v-model="pattern" />
    </div>
    <div
      class="q-gutter-y-md row q-my-sm items-center"
      style="max-width: 500px"
    >
      <p class="text-h5 q-mr-xl">Execution:</p>
      <q-input bg-color="white" filled v-model="execution" />
    </div>
    <div v-if="stocks">
      <p v-for="(stock, id) in stocks" :key="id">{{ stock.stock }}</p>
      <button @click="postFetchData">click to fetch</button>
    </div>
  </div>
</template>

<style lang="sass" scoped>
.bg-image
  height: 100vh
  background-image: url(../assets/stockBg.png)
  width: 100vw
p
  color: white
</style>

<script lang="ts">
import { defineComponent, PropType, computed, ref, toRef, Ref } from 'vue';
import { Todo, Meta } from './models';

export default defineComponent({
  name: 'CompositionComponent',
  data() {
    return {
      shares: '',
      sold: '',
      pattern: '',
      bought: '',
      execution: '',
      stockValue: '',
      stocks: {},
    };
  },
  methods: {
    postFetchData: async function () {
      const myData = {
        shares: this.shares,
        sold: this.sold,
        pattern: this.pattern,
        bought: this.bought,
        execution: this.execution,
        stock: this.stockValue,
      };
      const response = await fetch('http://localhost:3000/api', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(myData),
      });
      const data = await response.json();
      this.stocks = data.api;
      console.log(data, 'hello');
    },
    fetchData: async function () {
      const response = await fetch('http://localhost:3000/api');
      const data = await response.json();
      this.stocks = data;
      console.log(data, 'hello');
    },
  },
  created() {
    this.fetchData();
  },
});
</script>
