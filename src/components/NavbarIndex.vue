<template>
    <div id="nav-bar">
        <h1>WELCOME TO MY STORE</h1>
        <router-link :to="{ name: 'product' }" id="products-link">
        <button>List Product</button>
        </router-link>
        <router-link :to="{ name: 'cart' }" id="cart-link">
            <button>Cart</button>
        </router-link>
    </div>
</template>

<script>
export default {

}
</script>

<style scoped>
h1{
    text-align: center;
    color: black;
    font-size: 35px;
    margin: 0;
}

#nav-bar {
    border-bottom: 1px solid #ddd;
    height: 75px;
    width: 100%;
}

#products-link {
    text-align: center;
    display: block;
    color: #41B883;
    font-size: 22px;
    left: 32px;
    position: absolute;
    top: 28px;
    text-decoration: none;
}

#products-link h2 {
    margin: 2;
}

#cart-link {
    position: absolute;
    right: 16px;
    top: 28px;
}
</style>