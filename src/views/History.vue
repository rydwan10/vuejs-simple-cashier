<template>
  <div>
    <Navbar />
    <div class="container mt-3">
      <div class="row justify-content-center">
        <div v-for="item in history" :key="item.id" class="col-sm-6 mb-2">
          <div class="card" style="width: 100%;">
            <img src="../assets/logo.png" class="card-img-top ml-2 mt-2" style="width: 50px;" />
            <div class="card-body">
              <h5 class="card-title">{{ item.customer }}</h5>
              <p>
                <strong>Date: {{ item.date }}</strong>
              </p>
              <button
                type="button"
                data-toggle="modal"
                :data-target="`#modal_customer_`+item.id"
                class="btn btn-primary"
              >See Details</button>
            </div>
          </div>
          <!-- insert data into modal -->
          <div
            class="modal fade"
            :id="`modal_customer_`+item.id"
            tabindex="-1"
            role="dialog"
            aria-labelledby="exampleModalLabel"
            aria-hidden="true"
          >
            <div class="modal-dialog modal-lg">
              <div class="modal-content">
                <div class="modal-header">
                  <h5 class="modal-title">Customer name: {{ item.customer }}</h5>
                  <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">&times;</span>
                  </button>
                </div>
                <div class="modal-body">
                  <div class="row mb-1">
                    <div class="col">
                      <strong>Item Name</strong>
                    </div>
                    <div class="col">
                      <strong>Price</strong>
                    </div>
                    <div class="col">
                      <strong>Qty</strong>
                    </div>
                    <div class="col">
                      <strong>Sub Total</strong>
                    </div>
                  </div>
                  <div v-for="itemInCart in item.items" :key="itemInCart.id">
                    <div class="row">
                      <div class="col">{{ itemInCart.name }}</div>
                      <div class="col">{{ itemInCart.price_per_unit }}</div>
                      <div class="col">{{ itemInCart.qty }}</div>
                      <div class="col">{{ itemInCart.sub_total }}</div>
                    </div>
                  </div>
                  <div>
                    <hr />
                    <div class="row">
                      <div class="col"></div>
                      <div class="col"></div>
                      <div class="col">
                        <strong>Total Price</strong>
                      </div>
                      <div class="col">
                        <strong>{{ item.total_price }}</strong>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="modal-footer">
                  <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                  <button type="button" class="btn btn-primary">Re-print invoice</button>
                </div>
              </div>
            </div>
          </div>
          <!-- end of modal -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Footer from "@/components/Footer.vue";
export default {
  name: "History",
  components: {
    Navbar,
    Footer,
  },
  data() {
    return {
      history: [
        {
          id: 1,
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
            {
              id: 6,
              product_id: 5,
              name: "Carrot",
              qty: 4,
              unit: "kg",
              price_per_unit: 30000,
              sub_total: 120000,
            },
            {
              id: 7,
              product_id: 5,
              name: "Carrot",
              qty: 4,
              unit: "kg",
              price_per_unit: 30000,
              sub_total: 120000,
            },
            {
              id: 8,
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
        {
          id: 2,
          customer: "Anita",
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
        {
          id: 3,
          customer: "Jack Hilbert",
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
        {
          id: 4,
          customer: "Kimberly Hannah",
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
  computed: {
    countTotal() {
      let total = 0;
      this.history.items.forEach((item) => {
        return (total += item.sub_total);
      });
    },
  },
};
</script>

<style>
</style>