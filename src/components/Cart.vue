<template>
  <div class="card mb-3">
    <div class="card-header bg-white">
      <h3 class="card-title float-left">Cart</h3>
      <button @click="clearCart" class="btn btn-danger float-right">Clear Cart</button>
    </div>
    <div class="card-body table-responsive">
      <table class="table">
        <thead class="thead-dark">
          <tr>
            <th scope="col">#</th>
            <th scope="col">Name</th>
            <th scope="col">Qty</th>
            <th scope="col">Unit</th>
            <th scope="col">Price Per Unit</th>
            <th scope="col">Sub Total</th>
            <th scope="col">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in cart" :key="item.id">
            <th scope="row">{{ index + 1 }}</th>
            <td
              style="padding-right: 20px;"
              @dblclick="editName(item)"
              v-if="item.editing == false"
            >{{ item.name }}</td>
            <td style="width: 180px;" v-else>
              <input
                class="form-control"
                type="text"
                v-model="item.name"
                v-focus
                @keyup.enter="doneEditName(item)"
                @keyup.esc="cancelEditName(item)"
                @blur="doneEditName(item)"
              />
            </td>
            <td style="width: 130px;">
              <input class="form-control" type="number" v-model="item.qty" />
            </td>
            <td style="width: 110px;">
              <select v-model="item.unit" class="form-control" name="unit" id="unit">
                <option value="kg">Kg</option>
                <option value="ons">Ons</option>
                <option value="litre">Litre</option>
                <option value="pcs">Pcs</option>
                <option value="bag">Bag</option>
              </select>
            </td>
            <td style="width: 150px;">
              <input class="form-control" type="number" v-model="item.price_per_unit" />
            </td>
            <td>{{ item.qty * item.price_per_unit }}</td>
            <td>
              <button @click="deleteItem(index)" class="btn btn-danger">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="card-footer">
      <h4 class="float-right">Total Price: {{ total }}</h4>
    </div>
  </div>
</template>

<script>
export default {
  name: "Cart",
  props: ["cart"],
  data() {
    return {
      nameBeforeEdit: "",
    };
  },
  methods: {
    deleteItem(index) {
      this.$emit("deleteItem", index);
    },
    clearCart() {
      this.$emit("clearCart");
    },
    // Edit name of item
    editName(item) {
      this.nameBeforeEdit = item.name;
      item.editing = true;
    },
    doneEditName(item) {
      if (item.name.trim() == "") {
        item.name = this.nameBeforeEdit;
      }
      item.editing = false;
    },
    cancelEditName(item) {
      if (item.name.trim() == "") {
        item.name = this.nameBeforeEdit;
      }
      item.editing = false;
      item.name = this.nameBeforeEdit;
    },
  },
  computed: {
    total() {
      let total = 0;
      this.cart.forEach((item) => {
        total += item.qty * item.price_per_unit;
      });
      return total;
    },
  },
  directives: {
    focus: {
      inserted: function (el) {
        el.focus();
      },
    },
  },
};
</script>

<style scoped>
</style>