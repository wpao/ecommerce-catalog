<script>
import ProductDisplay from './components/ProductDisplay.vue'

export default {
  components: {
    ProductDisplay
  }
}
</script>

<template>
  <main>
    <ProductDisplay />
  </main>
</template>

<style scoped>
main{
  display: flex;
  justify-content: center;
}
</style>
