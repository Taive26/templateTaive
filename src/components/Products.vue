<template>
  <div>
    <h3 class="mb-3">Tooted</h3>
    <!-- TOODETE TABEL -->
    <b-table striped hover :items="items" :fields="fields">
      <template #cell(price)="data">
        <b class="text-info">{{ data.value }} EUR</b>
      </template>
      <!-- Nupp lisainfoks -->
      <template #cell(moreInfo)="data">
        <b-button
          v-b-modal.modal-1
          variant="success"
          @click="showInfo(data.item.productName, data.item.description)"
          >Lisainfo</b-button
        >
      </template>
    </b-table>

    <!-- LISAINFO -->
    <b-modal id="modal-1" :title="descriptionModalName" size="xl">
      <p>{{ productDescription }}</p>
    </b-modal>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Products",
  data() {
    return {
      fields: [
        { key: "type", label: "Toote liik:" },
        { key: "productName", label: "Toode:" },
        { key: "size", label: "Suurus:" },
        { key: "sizeUnit", label: "Ühik:" },
        { key: "price", label: "Hind:" },
        { key: "moreInfo", label: " " },
      ],
      items: [],
      descriptionModalName: "productName",
      productDescription: "description",
    };
  },
  async created() {
    const products = await axios({
      url: `api/products`,
      method: `GET`,
      headers: {},
    });
    console.log(products); //selleks, et vaadata, milline info sisse tuleb
    this.items = products.data.allProducts;
  },
  methods: {
    showInfo(productName, description) {
      this.descriptionModalName = productName;
      this.productDescription = description;
    },
  },
};
</script>

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
