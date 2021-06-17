<template>
  <div class="total-value" :class="classTotal">Balance: {{ total }}</div>
</template>

<script>
export default {
  name: "TotalBalance",
  props: {
    total: {
      type: Number,
      default: 0
    }
  },
  computed: {
    classTotal() {
      if (this.total > 0){
        return 'green';
      }
      else if (this.total < 0) {
        return 'red';
      }
      return 'black';
    }
  }
};
</script>

<style scoped>
.total-value {
  font-size: 1.5rem;
  text-transform: uppercase;
  padding: 1.25rem;
  text-align: center;
}
</style>
