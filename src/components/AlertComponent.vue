<template>
  <div class="alert" :class="alertType">{{ message }}</div>
</template>

<script>
export default {
  name: "AlertComponent",
  props: {
    // msg: String
    alertType: String,
    message: String,
  },
};
</script>

<style scoped>
.alert {
  position: fixed;
  top: 30px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 100000;
  pointer-events: none;
}
</style>
