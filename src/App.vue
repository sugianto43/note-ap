<template>
  <div id="app">
    <!-- HEADER COMPONENT -->
    <div class="header-title">
      <p class="label">Diari Jajan Bulan Februari</p>
      <p>Pengeluaran bulan ini Rp 5.605.475</p>

      <b-button variant="primary" @click="showModal = !showModal"
        >TAMBAH ITEM</b-button
      >

      <!-- MODAL ADD ITEM -->
      <b-modal v-model="showModal" hide-footer hide-header centered class="p-5">
        <h4>Tambah Entri</h4>
        <br />

        <label for="name">Nama</label>
        <b-form-input id="name" type="text" v-model="name" />

        <br />

        <label for="price">Harga</label>
        <b-form-input id="price" type="number" v-model="price" />

        <div class="btn-wrapper">
          <b-button class="cancel-btn" @click="handleCancelAdd">BATAL</b-button>
          <b-button variant="primary">KIRIM</b-button>
        </div>
      </b-modal>
      <!-- END OF MODAL ADD ITEM -->
    </div>
    <!-- END OF HEADER COMPONENT -->

    <!-- CONTENT -->
    <div class="content-wrapper">
      <CardItem />
      <CardItem />
      <CardItem />
      <CardItem />
      <CardItem />
    </div>
    <!--END OF CONTENT -->
  </div>
</template>

<script>
import CardItem from "./components/CardItem.vue";
export default {
  name: "App",
  components: {
    CardItem,
  },
  data() {
    return {
      showModal: false,
      name: "",
      price: null,
    };
  },
  methods: {
    handleCancelAdd() {
      this.showModal = false;
      this.name = "";
      this.price = null;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.header-title {
  text-align: center;
  padding: 30px;
}

.modal-body {
  padding: 20px !important;
}

.label {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 0;
}

.btn-wrapper {
  display: flex;
  justify-content: flex-end;
  margin-top: 20px;
}

.cancel-btn {
  margin-right: 15px;
}

.content-wrapper {
  display: grid;
  padding: 40px 30px;
  width: 100%;
  max-width: 1250px;
  margin: 0 auto;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  grid-auto-rows: auto;
  grid-gap: 1rem;
}
</style>
