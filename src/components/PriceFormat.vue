<template>
  <span>{{ price | currency }} </span>
</template>
<script>
export default {
  name: "PriceFormat",
  props: ["price"],
  filters: {
    currency: function (price) {
      return "₱ " + price.toFixed(2);
    },
  },
};
</script>
