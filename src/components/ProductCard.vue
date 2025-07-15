<template>
  <div class="card" @click="$emit('click')">
    <img :src="product.image" alt="image" class="product-img" />
    <h3>{{ product.title.slice(0, 20) }}...</h3>
    <p class='btn btn-outline-success'>Price: ${{ product.price }}</p>
  </div>
</template>

<script>
export default {
  props: ['product']
}
</script>

<style scoped>
.card {
  width: 200px;
  padding: 1rem;
  border: 1px solid #ddd;
  cursor: pointer;
  border-radius: 8px;
  text-align: center;
  object-fit: cover;
  margin-left: 1rem;
}
.product-img {
    
  width: 100px;
  height: 100px;
  object-fit: contain;
  
}
</style>
