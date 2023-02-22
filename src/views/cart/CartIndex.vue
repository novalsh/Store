<template>
  <div>
    <div id="page-wrap">
      <h1>Shoping Cart</h1>
      <h4 v-if="notif" class="notif">Item berhasil di hapus</h4>
      <CartItem v-for="item in cartItems" :key="item.id" :item="item" v-on:remove-item="removeFromCart($event)" />
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
  methods: {
    async removeFromCart(product) {
      await axios.delete(
        `http://localhost:8000/api/orders/user/1/product/${product}`
      )
      let indexCart = this.cartItems.map(function (item) {
        return item.code
      }).indexOf(product)
      this.cartItems.splice(indexCart, 1)
      this.notif = true
      setTimeout(() => {
        this.notif = false
      }, 2000)
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
.notif {
  color: green;
  font-size: 16px;
  font-weight: bold;
  margin: 0;
  padding: 16px;
  text-align: center;
}
</style>