<template>
  <div id="app">
    <AlertComponent :message="alertText" :alertType="alertType" />
    <NavBar
      :cart="cart"
      :cartState="cartState"
      @toggleCart="toggleCart"
      @closeCart="toggleCart"
      @minusToCart="minusToCart"
    ></NavBar>
    <ProductList
      :products="products"
      :maximum="maximum"
      @addToCart="addToCart"
    ></ProductList>
  </div>
</template>

<script>
import NavBar from "./components/NavBar.vue";
import ProductList from "./components/ProductList.vue";
import AlertComponent from "./components/AlertComponent.vue";

export default {
  name: "App",
  data: function () {
    return {
      maximum: 100,
      products: [],
      cart: [],
      cartState: false,
      alertText: "",
      alertType: "",
    };
  },
  methods: {
    showAlert: function (alertType, message) {
      this.alertText = message;
      this.alertType = alertType;

      setTimeout(() => {
        this.alertText = "";
        this.alertType = "";
      }, 2000);
    },
    toggleCart: function () {
      this.cartState = !this.cartState;
    },
    addToCart: function (item) {
      const existingItem = this.cart.find((cartItem) => cartItem.item === item);

      if (existingItem) {
        existingItem.qty++;
        this.showAlert("alert-success", "Incremented!");
      } else {
        this.cart.push({ item: item, qty: 1 });
        this.showAlert("alert-success", "Item Added!");
      }
    },
    minusToCart: function (cartId) {
      if (this.cart[cartId].qty > 1) {
        this.cart[cartId].qty -= 1;
        this.showAlert("alert-success", "Decremented!");
      } else {
        this.cart.splice(cartId, 1);
        this.showAlert("alert-success", "Deleted!");
      }
    },
  },
  computed: {},
  mounted: function () {
    fetch("https://dummyjson.com/products")
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
      });
  },
  components: {
    NavBar,
    ProductList,
    AlertComponent,
  },
};
</script>

<style></style>
