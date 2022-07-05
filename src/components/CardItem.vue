<template>
  <b-card class="shadow-sm">
    <h6 class="date">14 Februari</h6>
    <div class="card-item">
      <div class="time">09:20</div>
      <div class="title">Ayam Goreng</div>
      <div class="price">Rp 25.000</div>
    </div>

    <div class="card-item">
      <div class="time">09:20</div>
      <div class="title">Ayam Goreng</div>
      <div class="price">Rp 25.000</div>
    </div>

    <div class="card-item">
      <div class="time">09:20</div>
      <div class="title">Ayam Goreng</div>
      <div class="price">Rp 25.000</div>
    </div>

    <div class="total-price">
      <p>Total</p>
      <p class="value-price">Rp 544.987</p>
    </div>
  </b-card>
</template>

<script>
export default {
  name: "CardItem",
  props: {},
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
}

.price {
  width: 25%;
  text-align: right;
  font-size: 14px;
}

.total-price {
  display: flex;
  justify-content: flex-end;
  border-top: 2px solid rgba(128, 128, 128, 0.3);
  font-weight: bold;
  padding: 15px 10px 0 10px;
  font-size: 14px;
}

.value-price {
  margin-left: 40px;
}
</style>