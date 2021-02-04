<template>
  <div>
    <h2 class="mb-3">Tellimused</h2>

    <!--<p>Count: {{ count }}</p>
    <button @click="addCount()">+</button>
    <button @click="removeCount()">-</button> -->

    <b-table striped hover :items="items" :fields="fields">
    <!-- TELLIMUSTE TABEL -->   
      <template #cell(client)="data">
        <b class="text-info">{{ data.value.lastName }}</b
        >, <b>{{ data.value.firstName }}</b>
      </template>

      <!-- nupp toodete tabeli ilmumiseks -->
      <template #cell(actions)="data">
        <b-button variant="success" @click="showProducts(data.item.products)"
          >Vaata tooteid</b-button
        >
      </template>
    </b-table>
 <!-- TOOTE TABEL -->
  <!-- lisada reaalsed toodete kirjed -->
    <b-table striped hover :items="productItems" :fields="productFields">
    </b-table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Orders",
  data() {
    return {
      count: 0,
      fields: ["client", "products", "actions"],
      items: [],
      productItems: [],
      productFields: [],
    };
  },
  async created() {
    const orders = await axios({
      url: `api/orders`,
      method: `GET`,
      headers: {},
    });
    console.log(orders);
    this.items = orders.data.allOrders;
  },
  methods: {
    addCount() {
      this.count++;
    },
    removeCount() {
      this.count--;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
