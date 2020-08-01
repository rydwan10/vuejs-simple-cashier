<template>
  <div class="card">
    <div class="card-header bg-white">
      <h3>Payment</h3>
    </div>
    <div class="card-body">
      <div class="form-group">
        <label for="customer_name">Customer Name:</label>
        <input
          type="text"
          name="customer_name"
          id="customer_name"
          class="form-control"
          v-model="customer"
        />
      </div>
      <h6>Total Price:</h6>
      <h3>{{ totalPrice }}</h3>
      <div class="form-group">
        <label for="pay">Pay</label>
        <input type="number" name="pay" id="pay" class="form-control" v-model="pay" />
      </div>
      <h6>Change:</h6>
      <h5 v-if="paymentMessage" class="text-danger">Payment is less than the total price!</h5>
      <h3 :class="[checkField ? 'text-danger': 'text-success']">{{ calculateChange }}</h3>
      <button
        :class="[checkField ? 'disabled' : '']"
        :style="[checkField ? {cursor: 'not-allowed'} : '']"
        class="btn btn-success btn-block"
        @click="processPayment"
      >Pay</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Payment",
  props: ["cart"],
  data() {
    return {
      pay: "",
      customer: "",
    };
  },
  computed: {
    totalPrice() {
      let total = 0;
      this.cart.forEach((item) => {
        total += item.qty * item.price_per_unit;
      });
      return total;
    },
    calculateChange() {
      if (this.pay <= 0 || this.pay == "") {
        return "-";
      }
      return this.pay - this.totalPrice;
    },
    checkField() {
      if (this.pay < this.totalPrice || this.totalPrice == 0) {
        return true;
      }
      return false;
    },
    paymentMessage() {
      if (this.pay == "" || this.pay <= 0) {
        return false;
      } else if (this.pay > this.totalPrice) {
        return false;
      }
      return true;
    },
  },
  methods: {
    processPayment() {
      if (this.pay == "" || this.pay <= 0 || this.pay < this.totalPrice) {
        return;
      } else {
        // TODO i'll do it later :)
      }
    },
  },
};
</script>

<style>
</style>