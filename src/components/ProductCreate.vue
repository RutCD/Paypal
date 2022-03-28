<template>
  <div class="row justify-content-center">
    <div class="col-md-6">
      <h3 class="text-center">Add Product</h3>
      <form @submit.prevent="onFormSubmit">
        <div class="form-group">
          <label>Name</label>
          <input
            type="text"
            name="form-control"
            v-model="product.name"
            required
          />
        </div>
        <div class="form-group">
          <label>Precio</label>
          <input
            type="text"
            name="form-control"
            v-model="product.price"
            required
          />
        </div>
        <div class="form-group">
          <button class="btn btn-primary btn-block">Add product</button>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import { db } from "../firebase";
export default {
  data() {
    return {
      product: {
        name: "",
        price: "",
      },
    };
  },
  methods: {
    onFormSubmit(event) {
      //alert(JSON.stringify(this.product));
      event.preventDefault();
      db.collection("products")
        .add(this.product)
        .then(() => {
          alert("Product successfully crested!");
          this.product.name = "";
          this.product.price = "";
          if (!window.confirm("De you want add a new item?")) {
            this.$router.push("/listProduct");
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
