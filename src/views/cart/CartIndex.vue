<template>
  <div>
    <div id="page-wrap">
      <h1>Shoping Cart</h1>
      <CartItem
        v-for="item in cartItems"
        :key="item.id"
        :item="item"
      />
      <h3 id="total-price">Total: Rp.{{ totalPrice }}.000</h3>
      <button id="checkout-button">Checkout</button>
    </div>
  </div>
</template>

<script>
import CartItem from '../../components/CartItem'
import axios from 'axios'

export default {
  components: {
    CartItem
  },
  data() {
    return {
      cartItems: []
    }
  },
  computed: {
    totalPrice() {
      return this.cartItems.reduce(
        (sum, item) => sum + Number(item.price),
        0
      )
    } 
  },
  async created() {
    const result = await axios.get('http://localhost:8000/api/orders/user/1')
    let data = Object.assign({},
      ...(result.data.map(
        result => ({
        cart_items: result.products
        })
    ))
    )
    this.cartItems = data.cart_items
  }
}
</script>

<style scoped>

h1 {
    border-bottom: 1px solid #41B883;
    margin: 0;
    margin-top: 16px;
    padding: 16px;
  }
  #total-price {
    padding: 16px;
    text-align: right;
  }
  #checkout-button {
    width: 100%;
  }
</style>