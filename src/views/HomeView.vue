<template>
  <div class="splash-container">
    <div class="splash">
      <h1>Splendid Food</h1>
    </div>
  </div>

  <main class="wrapper">

    <h2>Recommended</h2>

    <div class="recommended">

      <ProductCardComponent v-for="(product, index) in inventory.slice(0,3)" :key="product.id" class="card"
        :index="index" :product="product" :addToCart="addToCart" />

    </div>

  </main>
</template>

<script>
// @ is an alias to /src
import ProductCardComponent from '@/components/ProductCardComponent.vue'
export default {
  name: 'HomeView',
  props: ['inventory', 'addToCart'],
  components: {
    ProductCardComponent
  }
}
</script>
