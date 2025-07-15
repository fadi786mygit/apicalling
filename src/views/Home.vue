<template>
  <div>
    <h2 class = 'd-flex justify-content-center align-items-center bg-black text-white m-2'>Welcome to Home Page</h2>
    <h3 class = 'd-flex justify-content-center align-items-center'>API Calling Example</h3>
    <div class="product-grid">
      <ProductCard
        v-for="product in filteredProducts"
        :key="product.id"
        :product="product"
        @click="viewProduct(product.id)"
      />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import ProductCard from '../components/ProductCard.vue'

export default {
  components: { ProductCard },

  data() {
    return {
      products: [],
      search: ''
    }
  },

  computed: {
    filteredProducts() {
      return this.products.filter(product =>
        product.title.toLowerCase().includes(this.search.toLowerCase())
      )
    }
  },

  watch: {
    search(newVal, oldVal) {
      console.log(`Search changed from "${oldVal}" to "${newVal}"`)
    }
  },

  async created() {
    const response = await axios.get('https://fakestoreapi.com/products')
    this.products = response.data
  },

  methods: {
    viewProduct(id) {
      this.$router.push(`/product/${id}`)
    }
  }
}
</script>

<style scoped>
.product-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 4rem;
}
</style>
