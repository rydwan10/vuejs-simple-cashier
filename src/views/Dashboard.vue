<template>
  <div class>
    <Navbar />
    <div class="container-fluid">
      <div class="row mt-3">
        <div class="col">
          <div v-if="this.cart.length == 0" class="card">
            <div class="card-header bg-white">
              <h3>Cart</h3>
            </div>
            <div class="card-body">
              <h4>Cart is empty...</h4>
            </div>
          </div>
          <Cart v-else :cart="cart" v-on:deleteItem="deleteItem" v-on:clearCart="clearCart" />
        </div>
        <div class="col-lg-4 col-md-6 col-sm-12">
          <AddItem class="mb-3" v-on:addItem="addItem" :products="products" />
          <Payment :cart="cart" />
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "@/components/Navbar.vue";
import AddItem from "@/components/AddItem.vue";
import Cart from "@/components/Cart.vue";
import Payment from "@/components/Payment.vue";
import Footer from "@/components/Footer.vue";

export default {
  name: "Dashboard",
  components: {
    Navbar,
    AddItem,
    Cart,
    Payment,
    Footer,
  },
  data() {
    return {
      products: [
        {
          id: 1,
          name: "Beef meat",
          stock: 100,
          unit: "kg",
          price_per_unit: 10000,
        },
        {
          id: 2,
          name: "Chicken thig",
          stock: 30,
          unit: "kg",
          price_per_unit: 154000,
        },
        {
          id: 3,
          name: "Egg",
          stock: 400,
          unit: "kg",
          price_per_unit: 20000,
        },
        {
          id: 4,
          name: "Cabbage",
          stock: 250,
          unit: "kg",
          price_per_unit: 40000,
        },
        {
          id: 5,
          name: "Carrot",
          stock: 400,
          unit: "kg",
          price_per_unit: 30000,
        },
      ],
      cart: [
        {
          id: 1,
          product_id: 1,
          name: "Beef meat",
          qty: 4,
          unit: "kg",
          price_per_unit: 10000,
          editing: false,
        },
        {
          id: 2,
          product_id: 2,
          name: "Chicken thig",
          qty: 1,
          unit: "kg",
          price_per_unit: 154000,
          editing: false,
        },
        {
          id: 3,
          product_id: 3,
          name: "Egg",
          qty: 1,
          unit: "kg",
          price_per_unit: 20000,
          editing: false,
        },
        {
          id: 4,
          product_id: 4,
          name: "Cabbage",
          qty: 2,
          unit: "kg",
          price_per_unit: 40000,
          editing: false,
        },
        {
          id: 5,
          product_id: 5,
          name: "Carrot",
          qty: 4,
          unit: "kg",
          price_per_unit: 30000,
          editing: false,
        },
      ],
      history: [
        {
          customer: "John Doe",
          cashier: "Natalia Nirana",
          date: "2020-07-25",
          items: [
            {
              id: 1,
              product_id: 1,
              name: "Beef meat",
              qty: 4,
              unit: "kg",
              price_per_unit: 10000,
              sub_total: 40000,
            },
            {
              id: 2,
              product_id: 2,
              name: "Chicken thigs",
              qty: 1,
              unit: "kg",
              price_per_unit: 154000,
              sub_total: 154000,
            },
            {
              id: 3,
              product_id: 3,
              name: "Eggs",
              qty: 1,
              unit: "kg",
              price_per_unit: 20000,
              sub_total: 20000,
            },
            {
              id: 4,
              product_id: 4,
              name: "Cabbage",
              qty: 2,
              unit: "kg",
              price_per_unit: 40000,
              sub_total: 80000,
            },
            {
              id: 5,
              product_id: 5,
              name: "Carrot",
              qty: 4,
              unit: "kg",
              price_per_unit: 30000,
              sub_total: 120000,
            },
          ],
          total_price: 414000,
          payment_type: "cash",
          pay: 500000,
          tax: 0,
          change: 86000,
        },
      ],
    };
  },
  methods: {
    deleteItem(index) {
      this.cart.splice(index, 1);
    },
    clearCart() {
      if (this.cart.length == 0) {
        return;
      } else {
        let confirmDelete = confirm("Clear cart?");
        if (confirmDelete) {
          this.cart = [];
        }
      }
    },
    addItem(newItem) {
      this.cart.push(newItem);
    },
  },
};
</script>
