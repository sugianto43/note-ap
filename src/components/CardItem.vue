<template>
  <b-card class="shadow-sm">
    <h6 class="date">{{ date }}</h6>

    <div class="card-item" v-for="(item, idx) in notes" :key="idx">
      <div class="time">{{ item.jam }}</div>
      <div class="title">{{ item.nama }}</div>
      <div class="price">{{ formatPrice(item.pengeluaran) }}</div>
    </div>

    <div class="total-price">
      <p>Total</p>
      <p class="value-price">{{ formatPrice(totalPrice) }}</p>
    </div>
  </b-card>
</template>

<script>
export default {
  name: "CardItem",
  props: {
    id: String,
    date: String,
    total: String,
    notes: {
      typeof: Array,
      default: () => [],
    },
  },
  computed: {
    totalPrice() {
      let sum = this.notes.reduce((a, b) => {
        return a + b.pengeluaran;
      }, 0);
      return sum;
    },
  },
  methods: {
    formatPrice(value) {
      return "Rp " + value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    },
  },
};
</script>

<style scoped>
.card-item {
  display: flex;
  align-items: center;
  border-top: 1px solid rgba(128, 128, 128, 0.2);
  padding: 10px;
}

.date {
  font-weight: bold;
}

.time {
  width: 15%;
  font-size: 14px;
}

.title {
  width: 60%;
  font-size: 14px;
  padding-left: 10px;
  text-transform: capitalize;
}

.price {
  width: 25%;
  text-align: right;
  font-size: 14px;
}

.total-price {
  display: flex;
  justify-content: flex-end;
  border-top: 1.5px solid rgba(128, 128, 128, 0.3);
  font-weight: bold;
  padding: 15px 10px 0 10px;
  font-size: 14px;
}

.value-price {
  margin-left: 40px;
}
</style>