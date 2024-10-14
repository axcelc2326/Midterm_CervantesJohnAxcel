<template>
  <div class="app-container">
    <nav class="navbar">
      <router-link to="/home" class="nav-link" exact-active-class="active">Home</router-link>
      <router-link to="/products" class="nav-link" exact-active-class="active">Products</router-link>
    </nav>
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App'
};
</script>

<style scoped>
.app-container {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  min-height: 100vh;
}

.navbar {
  background-color: #007BFF;
  width: 100%;
  padding: 15px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.nav-link {
  color: white;
  text-decoration: none;
  margin: 0 15px;
  font-size: 1.2rem;
  transition: color 0.3s ease;
}

.nav-link:hover {
  color: #f0f0f0;
}

.active {
  font-weight: bold;
  border-bottom: 2px solid white;
}

.router-view {
  flex-grow: 1;
  padding: 20px;
  width: 100%;
  max-width: 800px;
}
</style>
