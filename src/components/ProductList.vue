<template>
  <div>
    <div
      class="item-container container card p-2 mt-3"
      v-for="item in products.products"
      :key="item.id"
    >
      <img :src="item.images['0']" />
      <div class="container">
        <h5>{{ item.title }}</h5>
        <h5><PriceFormat :price="item.price"></PriceFormat></h5>
        <p>{{ item.description }}</p>
        <button class="btn btn-light text-warning" @click="$emit('addToCart', item)">
          <i class="bi bi-cart-plus-fill"></i>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import PriceFormat from "./PriceFormat.vue";

export default {
  name: "ProductList",
  props: ["products", "maximum"],
  components: {
    PriceFormat,
  },
};
</script>

<style scoped>
button {
  font-size: 20px;
}
</style>
