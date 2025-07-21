<template>
  <div class="container">
    <div class="row">
      <div class="col-12 text-center">
        <h4 class="pt-3">Edit Product</h4>
      </div>
    </div>

    <div class="row">
      <div class="col-3"></div>
      <div class="col-md-6 px-5 px-md-0">
        <form>
          <div class="form-group">
            <label>Name</label>
            <input type="text" class="form-control" v-model="name" required />
          </div>
          <div class="form-group">
            <label>Description</label>
            <input type="text" class="form-control" v-model="description" required />
          </div>
          <div class="form-group">
            <label>Image URL</label>
            <input type="text" class="form-control" v-model="imageUrl" required />
          </div>
          <div class="form-group">
            <label>Price ($)</label>
            <input type="number" class="form-control" v-model.number="price" required />
          </div>
          <button type="button" class="btn btn-primary" @click="editProduct">Submit</button>
        </form>
      </div>
      <div class="col-3"></div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      id: null,
      name: null,
      description: null,
      imageUrl: null,
      price: null,
      categoryId: null,
    };
  },
  props: ["baseURL", "products"],
  methods: {
    async editProduct() {
      const updatedProduct = {
        id: this.id,
        name: this.name,
        description: this.description,
        imageUrl: this.imageUrl,
        price: this.price,
        categoryId: this.categoryId,
      };

      await axios({
        method: 'post',
        url: this.baseURL + "product/" + this.id,
        data: JSON.stringify(updatedProduct),
        headers: {
          'Content-Type': 'application/json',
        },
      })
        .then(() => {
          console.log("Product updated successfully!");
        })
        .catch((err) => console.log(err));
    },
  },
  mounted() {
    this.id = this.$route.params.id;
    const product = this.products.find(product => product.id == this.id);

    if (product) {
      this.name = product.name;
      this.description = product.description;
      this.imageUrl = product.imageUrl;
      this.price = product.price;
      this.categoryId = product.categoryId;
    }
  },
};
</script>
