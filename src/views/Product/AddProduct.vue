<template>
  <div class="container">
    <div class="row">
      <div class="col-12 text-center">
        <h4 class="pt-3">Add New Product</h4>
      </div>
    </div>

    <div class="row">
      <div class="col-3"></div>
      <div class="col-md-6 px-5 px-md-0">
        <form>
          <div class="form-group">
            <label>Category</label>
            <select class="form-control" v-model="categoryId" required>
              <option
                v-for="category in categories"
                :key="category.id"
                :value="category.id"
              >
                {{ category.categoryName }}
              </option>
            </select>
          </div>

          <div class="form-group">
            <label>Name</label>
            <input
              type="text"
              class="form-control"
              v-model="name"
              required
            />
          </div>

          <div class="form-group">
            <label>Description</label>
            <input
              type="text"
              class="form-control"
              v-model="description"
              required
            />
          </div>

          <div class="form-group">
            <label>Image URL</label>
            <input
              type="text"
              class="form-control"
              v-model="imageUrl"
              required
            />
          </div>

          <div class="form-group">
            <label>Price</label>
            <input
              type="number"
              class="form-control"
              v-model="price"
              required
            />
          </div>

          <button
            type="button"
            class="btn btn-primary"
            @click="addProduct"
          >
            Submit
          </button>
        </form>
      </div>
      <div class="col-3"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      categories: [],
      categoryId: null,
      name: "",
      description: "",
      imageUrl: "",
      price: null,
    };
  },
  methods: {
    async addProduct() {
      const newProduct = {
        categoryId: this.categoryId,
        name: this.name,
        description: this.description,
        imageUrl: this.imageUrl,
        price: this.price,
      };

      const baseURL = "http://localhost:8000/";

      try {
        await axios.post(baseURL + "product/", newProduct, {
          headers: {
            "Content-Type": "application/json",
          },
        });
        alert("Product added successfully!");
      } catch (error) {
        console.error("Error adding product:", error);
        alert("Failed to add product.");
      }
    },
    async fetchCategories() {
      try {
        const response = await axios.get("http://localhost:8000/category/");
        this.categories = response.data;
      } catch (error) {
        console.error("Error fetching categories:", error);
      }
    },
  },
  mounted() {
    this.fetchCategories();
  },
};
</script>

