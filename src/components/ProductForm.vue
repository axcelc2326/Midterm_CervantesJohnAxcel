<template>
  <form @submit.prevent="submitProduct" class="product-form">
    <h2>{{ isEditing ? 'Edit Product' : 'Add New Product' }}</h2>
    <div class="form-group">
      <label for="name">Product Name:</label>
      <input type="text" v-model="product.name" required class="form-input" />
    </div>
    <div class="form-group">
      <label for="price">Price:</label>
      <input type="number" v-model="product.price" required class="form-input" />
    </div>
    <div class="form-group">
      <label for="description">Description:</label>
      <textarea v-model="product.description" required class="form-textarea"></textarea>
    </div>
    <button type="submit" class="submit-button">{{ isEditing ? 'Update Product' : 'Add Product' }}</button>
  </form>
</template>

<script>
export default {
  props: {
    initialProduct: {
      type: Object,
      default: () => ({ name: '', price: 0, description: '' })
    }
  },
  data() {
    return {
      product: { ...this.initialProduct },
      isEditing: false
    };
  },
  watch: {
    initialProduct: {
      handler(newVal) {
        this.product = { ...newVal };
        this.isEditing = true;
      },
      immediate: true
    }
  },
  methods: {
    submitProduct() {
      this.$emit('add-product', { ...this.product });
      this.resetForm();
    },
    resetForm() {
      this.product = { name: '', price: 0, description: '' };
      this.isEditing = false;
      this.$emit('form-reset');
    }
  }
};
</script>

<style scoped>
.product-form {
  max-width: 500px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #ffffff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.product-form h2 {
  text-align: center;
  color: #333;
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 15px;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
  color: #555;
}

.form-input,
.form-textarea {
  width: 100%;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 16px;
  transition: border-color 0.3s ease;
}

.form-input:focus,
.form-textarea:focus {
  border-color: #007BFF;
  outline: none;
}

.form-textarea {
  resize: vertical;
  min-height: 100px;
}

.submit-button {
  width: 100%;
  padding: 12px;
  border: none;
  border-radius: 4px;
  background-color: #007BFF;
  color: white;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.submit-button:hover {
  background-color: #0056b3;
}
</style>
