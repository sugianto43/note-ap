<template>
  <div id="app">
    <!-- HEADER COMPONENT -->
    <div class="header-title">
      <p class="label">Diari Jajan Tahun 2022</p>
      <p>Pengeluaran bulan ini {{ formatPrice(total) }}</p>

      <b-button variant="primary" @click="handleShowModal"
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
          <b-button
            variant="primary"
            @click="handleAddItem"
            :disabled="!name || !price"
            >KIRIM</b-button
          >
        </div>
      </b-modal>
      <!-- END OF MODAL ADD ITEM -->
    </div>
    <!-- END OF HEADER COMPONENT -->

    <!-- CONTENT -->
    <div class="content-wrapper">
      <CardItem
        v-for="value in data"
        :key="value.id"
        :id="value.id"
        :date="value.date"
        :total="value.total"
        :notes="value.detail"
      />
    </div>
    <!--END OF CONTENT -->
  </div>
</template>

<script>
import CardItem from "./components/CardItem.vue";
import { uuid } from "vue-uuid";
import { format } from "date-fns";

export default {
  name: "App",
  components: {
    CardItem,
  },
  data() {
    return {
      data: [],
      showModal: false,
      name: "",
      price: null,
      total: null,
    };
  },
  watch: {
    // clear all input field when modal is closed
    showModal() {
      if (!this.showModal) {
        this.name = "";
        this.price = null;
      }
    },
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    formatPrice(value) {
      return "Rp " + value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    },
    totalCount(data) {
      let result = 0;
      for (let i = 0; i < data.length; i++) {
        for (let j = 0; j < data[i].detail.length; j++) {
          result += data[i].detail[j].pengeluaran;
        }
      }
      return result;
    },
    handleShowModal() {
      this.showModal = !this.showModal;
      console.log("open");
    },
    handleCancelAdd() {
      this.showModal = false;
      this.name = "";
      this.price = null;
    },
    handleAddItem() {
      let date = format(new Date(), "dd MMMM yyyy");
      let time = format(new Date(), "HH:mm");
      let isExist = this.data.some((item) => item.date === date);

      if (isExist) {
        let index = this.data.findIndex((item) => item.date === date);
        this.data[index].detail.push({
          jam: time,
          tanggal: date,
          nama: this.name,
          pengeluaran: Number(this.price),
        });
      } else {
        let newData = {
          id: uuid.v1(),
          date: date,
          detail: [
            {
              jam: time,
              tanggal: date,
              nama: this.name,
              pengeluaran: Number(this.price),
            },
          ],
        };
        let copyData = this.data.reverse();
        this.data = [...copyData, newData].reverse();
      }
      this.total = this.totalCount(this.data);
      this.showModal = false;
    },
    async fetchData() {
      let url = "http://localhost:3001/items";
      let res = await fetch(url);
      let result = await res.json();
      this.data = result.reverse();
      this.total = this.totalCount(this.data);
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
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  grid-auto-rows: auto;
  grid-gap: 1rem;
}
</style>
