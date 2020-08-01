<template>
  <div class="card">
    <div class="card-header bg-white">
      <h3 class="float-left">Add Item</h3>
      <!-- Button trigger modal -->
      <button
        type="button"
        class="btn btn-primary float-right"
        data-toggle="modal"
        data-target="#modelId"
      >Search Item</button>
    </div>
    <div class="card-body">
      <div class="form-group">
        <label for="name">Name</label>
        <input v-model="name" type="text" name="name" id="name" class="form-control" />
      </div>
      <div class="form-group">
        <label for="qty">Qty</label>
        <input v-model="qty" type="number" name="qty" id="qty" class="form-control" />
      </div>
      <div class="form-group">
        <label for="unit">Unit</label>
        <select v-model="unit" class="form-control" name="unit" id="unit">
          <option value="kg">Kg</option>
          <option value="ons">Ons</option>
          <option value="litre">Litre</option>
          <option value="pcs">Pcs</option>
          <option value="bag">Bag</option>
        </select>
      </div>
      <div class="form-group">
        <label for="price_per_unit">Price per Unit</label>
        <input
          v-model="price_per_unit"
          type="number"
          name="price_per_unit"
          id="price_per_unit"
          class="form-control"
        />
      </div>
      <div class="form-group">
        <h4>Sub total: {{ subTotal }}</h4>
      </div>
      <div class="form-group">
        <button
          v-on:click="addItem"
          :style="[checkField ? {cursor: 'not-allowed'} : '']"
          :class="{disabled: checkField}"
          class="btn btn-success btn-block"
        >Add</button>
      </div>
    </div>

    <!-- Modal -->
    <div
      class="modal fade"
      id="modelId"
      tabindex="-1"
      role="dialog"
      aria-labelledby="modelTitleId"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-xl" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">Product List</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="form-group row">
              <label for="search_product" class="col-sm-2 col-form-label">Search Product</label>
              <input
                type="text"
                name="search_product"
                id="search_product"
                class="form-control col-sm-5"
                placeholder="Search..."
              />
            </div>
            <table class="table">
              <thead class="thead-dark">
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Name</th>
                  <th scope="col">Stock</th>
                  <th scope="col">Unit</th>
                  <th scope="col">Price Per Unit</th>
                  <th scope="col">Action</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(item, index) in products" :key="item.id">
                  <td>{{ index+1 }}</td>
                  <td>{{ item.name }}</td>
                  <td>{{ item.stock }}</td>
                  <td>{{ item.unit }}</td>
                  <td>{{ item.price_per_unit }}</td>
                  <td>
                    <button data-dismiss="modal" class="btn btn-success">Choose</button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary">Save</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddItem",
  props: {
    products: Array,
  },
  data() {
    return {
      id: 9,
      name: "",
      qty: "",
      unit: "",
      price_per_unit: 0,
    };
  },
  computed: {
    subTotal() {
      if (this.qty <= 0 || this.price_per_unit <= 0) {
        return "-";
      }
      return this.qty * this.price_per_unit;
    },
    checkField() {
      if (
        this.name == "" ||
        this.qty == "" ||
        this.qty <= 0 ||
        this.unit == "" ||
        this.price_per_unit == "" ||
        this.price_per_unit <= 0
      ) {
        return true;
      }
    },
  },
  methods: {
    addItem(e) {
      if (
        this.name == "" ||
        this.qty == "" ||
        this.qty <= 0 ||
        this.unit == "" ||
        this.price_per_unit == "" ||
        this.price_per_unit <= 0
      ) {
        return;
      }
      const newItem = {
        id: this.id++,
        name: this.name,
        qty: this.qty,
        unit: this.unit,
        price_per_unit: this.price_per_unit,
        editing: false,
      };
      this.$emit("addItem", newItem);
      this.name = "";
      this.qty = 0;
      this.unit = "";
      this.price_per_unit = 0;
    },
  },
};
</script>

<style>
</style>