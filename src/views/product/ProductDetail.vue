<template>
  <div>
        <div id="page-wrap" v-if="product">
          <h4 v-if="notif" class="notif">Item telah ditambahkan ke dalam keranjang</h4>
          <div id="img-wrap">
            <img :src="`http://localhost:8000${product.imageUrl}`" alt="">
          </div>
          <div id="product-details">
            <h1>{{ product.name }}</h1>
            <h3 id="id-price">Rp.{{ product.price }}</h3>
            <p>AverageRating:{{ product.averageRating }}</p>
            <button id="add-to-cart" @click="addToCart(product.code)">Add to Cart</button>
            <p>{{ product.description  }}</p>
          </div>
        </div>
        <NotFound v-else />
  </div>
</template>

<script> 
import axios from 'axios';
import NotFound from '../errors/NotFound.vue';

export default {
  components: {
    NotFound
  },
  data() {
    return {
      product: {}, 
      notif: false
    }
  }, 
  methods: {
    async addToCart(product){
      await axios.post('http://localhost:8000/api/orders/update/user/1', {
        product: product
      }) 
      this.notif = true
    }
  },
  async created() {
    const code = this.$route.params.id;
    const result = await axios.get(`http://localhost:8000/api/products/${code} `)
    this.product = result.data 
  }
}
</script>


<style scoped>
 #page-wrap {
    margin-top: 16px;
    padding: 16px;
    max-width: 600px;
  }

  #img-wrap {
    text-align: center;
  }

  img {
    width: 400px;
  }

  #product-details {
    padding: 16px;
    position: relative;
  }

  #add-to-cart {
    width: 100%;
  }

  #price {
    position: absolute;
    top: 24px;
    right: 16px;
  } 

  .notif {
    background-color: #41B883;
    color: white;
    padding: 16px;
    text-align: center;
  }
</style>