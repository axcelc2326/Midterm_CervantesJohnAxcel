<template>
  <div class="product-list">
    <ul class="product-items">
      <li v-for="(product, index) in products" :key="index" class="product-item">
        <h3 class="product-name">{{ product.name }} - ${{ product.price }}</h3>
        <p class="product-description">{{ product.description }}</p>
        <button class="edit-button" @click="editProduct(index)">Edit</button>
      </li>
    </ul>
    <div v-if="editingIndex !== null" class="edit-form">
      <ProductForm 
        @add-product="updateProduct" 
        :initialProduct="products[editingIndex]" 
        @form-reset="resetEditing" 
      />
    </div>
  </div>
</template>

<script>
import ProductForm from './ProductForm.vue';

export default {
  components: {
    ProductForm
  },
  props: {
    products: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      editingIndex: null
    };
  },
  methods: {
    editProduct(index) {
      this.editingIndex = index;
    },
    updateProduct(updatedProduct) {
      this.$emit('update-product', { index: this.editingIndex, product: updatedProduct });
      this.resetEditing();
    },
    resetEditing() {
      this.editingIndex = null; // reset after update
    }
  }
};
</script>

<style scoped>
.product-list {
  max-width: 600px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background-color: #f9f9f9;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

.product-items {
  list-style: none;
  padding: 0;
  margin: 0;
}

.product-item {
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 15px;
  margin-bottom: 10px;
  background-color: #fff;
  transition: box-shadow 0.3s;
}

.product-item:hover {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.product-name {
  margin: 0;
  color: #333;
}

.product-description {
  color: #666;
}

.edit-button {
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  background-color: #007BFF;
  color: white;
  cursor: pointer;
  transition: background-color 0.3s;
}

.edit-button:hover {
  background-color: #0056b3;
}

.edit-form {
  margin-top: 20px;
  border-top: 2px solid #007BFF;
  padding-top: 20px;
}
</style>
