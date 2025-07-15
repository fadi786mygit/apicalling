<template>
  <div v-if="product" class="container mt-5">
    <div class="row">
    <div class="col-6">
    <img :src="product.image" class="detail-img d-flex col-6" /> </div>
    <div class="d-flex flex-column col-6">
    <h1>{{ product.title }}</h1>
    <p><strong>Price:</strong> ${{ product.price }}</p>
    <p><strong>Description:</strong> {{ product.description }}</p>
    <p><strong>Category:</strong> {{ product.category }}</p>
    <p><strong>Rating:</strong> {{ product.rating.rate }} ({{ product.rating.count }} reviews)</p>
    <div class="d-flex justify-content-center gap-2 align-items-center mt-1">
    <button class ='btn btn-danger' @click="decrementCount">-</button>
     <h4>{{ count }}</h4>
    <button class ='btn btn-success' @click="incrementCount">+</button>
    <button class ='btn btn-primary' @click='addtocart'>Add to Cart</button>
    </div>
    </div>
  </div>
  </div>
</template>

<script>
import axios from 'axios'
import { Alert } from 'react-bootstrap'

export default {
  data() {
    return {
      product: null,
      count: 0
    }
  },
  async created() {
    const id = this.$route.params.id
    const res = await axios.get(`https://fakestoreapi.com/products/${id}`)
    this.product = res.data
  },

  methods: {
    incrementCount() {
      this.count++
    },
    decrementCount() {
      if (this.count > 0) {
        this.count--
      }
    },
    addtocart() {
      if (this.count > 0) {
        window.alert(`${this.product.title} added to cart! Quantity: ${this.count}`)
      } else {
        window.alert('Please select a quantity before adding to cart.')
      }
    }
  }
}

</script>

<style scoped>
.detail-img {
  width: 300px;
  height: 300px;
  margin-bottom: 1rem;
}


</style>
