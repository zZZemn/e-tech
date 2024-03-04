<template>
  <div>
    <nav class="d-flex justify-content-between align-items-center p-2 bg-dark">
      <a href="/" class="text-decoration-none text-light">E-Tech</a>
      <button class="btn text-light" @click="$emit('toggleCart')">
        <i class="bi bi-cart-fill"></i>
        <span class="badge badge-pill bg-danger text-light">{{
          cart.length
        }}</span>
      </button>
    </nav>
    <div class="cart-container container p-2">
      <div class="card p-3 pt-4" v-if="cartState">
        <button
          class="btn-close-cart btn btn-light"
          @click="$emit('closeCart')"
        >
          <i class="bi bi-x-lg"></i>
        </button>
        <h5 class="text-center">Cart</h5>
        <hr />
        <div class="cart-items-container">
          <div class="mt-1 d-flex" v-for="(item, index) in cart" :key="index">
            <img :src="item.item.images[0]" />
            <div
              class="title-container d-flex px-2 w-100 justify-content-between align-items-center"
            >
              <p class="m-0">
                {{ item.item.title }} <br />
                <PriceFormat :price="item.item.price" />
                <br />
                <span class="text-success">{{ item.qty }} pc/s</span>
              </p>
              <button
                class="btn-minus-cart btn btn-danger"
                @click="$emit('minusToCart', index)"
              >
                -
              </button>
            </div>
          </div>
        </div>
        <div
          class="total-value-container bg-light d-flex justify-content-between align-items-center rounded p-2 mt-3"
          v-if="cart.length > 0"
        >
          <h6 class="m-0">Total:</h6>
          <h6 class="m-0"><PriceFormat :price="totalValueInCart" /></h6>
        </div>
        <h6 class="text-center text-danger" v-if="cart.length < 1">
          Your Cart is Empty.
        </h6>
      </div>
    </div>
  </div>
</template>

<script>
import PriceFormat from "./PriceFormat.vue";

export default {
  name: "NavBar",
  methods: {},
  props: ["cart", "cartState"],
  computed: {
    totalValueInCart: function () {
      let cartTotalVal = 0;
      for (const item in this.cart) {
        cartTotalVal += this.cart[item].qty * this.cart[item].item.price;
      }

      return cartTotalVal;
    },
  },
  components: {
    PriceFormat,
  },
};
</script>

<style scoped>
nav {
  position: sticky;
  top: 0;
  z-index: 1000;
}

nav a {
  font-size: 25px;
}

nav button {
  font-size: 30px;
  position: relative;
  padding: 0 10px;
}

.badge {
  font-size: 10px;
  position: absolute !important;
  top: 0;
  right: 0;
}

.cart-container {
  position: absolute;
  z-index: 1000;
}

.cart-items-container {
  max-height: 300px !important;
  overflow-y: auto;
}

img {
  height: 60px;
  width: 60px;
}

.title-container {
  font-size: 13px;
}

.btn-minus-cart {
  padding: 5px;
}

.btn-close-cart {
  position: absolute;
  top: 1px;
  right: 1px;
}
</style>
