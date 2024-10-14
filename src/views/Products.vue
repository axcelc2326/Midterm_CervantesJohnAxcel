<template>
  <div>
    <ProductForm @add-product="addProduct" />
    <ProductList :products="products" @update-product="updateProduct" />
  </div>
</template>

<script>
import ProductForm from '../components/ProductForm.vue';
import ProductList from '../components/ProductList.vue';

export default {
  components: {
    ProductForm,
    ProductList,
  },
  data() {
    return {
      products: []
    };
  },
  methods: {
    addProduct(product) {
      this.products.push(product);
    },
    updateProduct({ index, product }) {
      this.$set(this.products, index, product);
    }
  }
};
</script>

<style scoped>
/* Add any additional styles for the parent component here */
</style>
