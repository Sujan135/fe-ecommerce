<template>
  <div class="container">
    <div class="row">
      <div v-for="product of products" :key="product.id" class="col-md-6 col-xl-4 col-12 pt-3 justify-content-around d-flex">
        <div class="card" style="width: 18rem;">
          <img :src="product.imageUrl" class="card-img-top" alt="product image" />
          <div class="card-body">
            <h5 class="card-title">{{ product.name }}</h5>
            <p class="card-text">{{ product.description }}</p>
            <ul class="list-group list-group-flush">
              <li class="list-group-item">{{ product.price }}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductList",
  props: ["baseURL", "products"],
  mounted() {
  }
}
</script>

<style scoped>
h5 {
  font-family: 'Roboto', sans-serif;
  color: #484848;
  font-weight: 700;
}
</style>
