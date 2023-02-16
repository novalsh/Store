<template>
  <div>
    <div id="page-wrap">
      <div class="grip-wrap">
        <ProductItem
        v-for="product in products"
        :key="product.id"
        :product="product"
        />
      </div>
    </div>
  </div>
</template>

<script>
import ProductItem from '../../components/ProductItem';
import { products } from '../../data-seed';
export default {
  data() {
    return {
      products
    }
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