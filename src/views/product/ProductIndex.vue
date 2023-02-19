<template>
  <div>
    <div id="page-wrap">
      <div class="grip-wrap">
        <ProductItem v-for="product in products" :key="product.id" :product="product" />
      </div>
    </div>
  </div>
</template>

<script>
import ProductItem from '../../components/ProductItem'
import axios from 'axios'
export default {
  data() {
    return {
      products: []
    }
  },
  async created() {
    const result = await axios.get('http://localhost:8000/api/products')
    this.products = result.data
  },
  components: {
    ProductItem
  }
}
</script>

<style scoped >
.grip-wrap {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin-top: 16px;
}
</style>