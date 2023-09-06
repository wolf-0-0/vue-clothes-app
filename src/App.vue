<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <router-link to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </router-link>
      <router-link to="/products" class="top-bar-link">
        <span>Products</span>
      </router-link>
      <router-link to="/past-orders" class="top-bar-link">
        <span>Past Orders</span>
      </router-link>
    </nav>
    <div @click="toggleSidebar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <span>Cart ({{ totalQuantity }})</span>
    </div>
  </header>
  <router-view :inventory="inventory" :addToCart="addToCart" />

  <SidebarComponent v-if="showSidebar" :toggle="toggleSidebar" :cart="cart" :inventory="inventory" :remove="removeItem" />
</template>

<script>
// @ for reference to the src folder
import SidebarComponent from '@/components/SidebarComponent.vue'
// import food from './food.json'
import products from './products.json'

// Options object
export default {
  components: {
    SidebarComponent
  },
  data () {
    return {
      showSidebar: false,
      inventory: {},
      cart: {}
    }
  },
  computed: {
    totalQuantity () {
      return Object.values(this.cart).reduce((sum, curr) => {
        return sum + curr
      }, 0)
    }
  },
  methods: {
    addToCart (name, quantity) {
      if (!this.cart[name]) this.cart[name] = 0
      this.cart[name] += quantity
    },
    toggleSidebar () {
      this.showSidebar = !this.showSidebar
    },
    removeItem (name) {
      delete this.cart[name]
    },
    async fetchProducts () {
    // const url = 'https://asos2.p.rapidapi.com/products/v2/list?limit=48&categoryId=4209&offset=0&store=US&lang=en-US&sizeSchema=US&currency=USD&sort=freshness&country=US'
    // const options = {
    //   method: 'GET',
    //   headers: {
    //     'X-RapidAPI-Key': '5ca79e48a1msh354f59a6345499fp1f06cdjsn2930d1c46d0d',
    //     'X-RapidAPI-Host': 'asos2.p.rapidapi.com'
    //   }
    // }
      try {
        // const response = await fetch(url, options)
        // const result = await response.json()
        const result = products
        console.log(result.categoryName);
        console.log(result.products);
        this.inventory = result.products;
      } catch (error) {
        console.error(error)
      }
    }
  },
  mounted() {
    this.fetchProducts()
  }
}
</script>
<!-- scoped keyword makes that styles only apply to this componenet -->
<!-- <style scoped>
</style> -->
