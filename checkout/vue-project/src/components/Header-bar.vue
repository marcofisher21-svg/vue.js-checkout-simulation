<script setup>
const props = defineProps({
  count: {
    type: Number,
    default: 0
  }
})
</script>

<template>
  <header class="navbar">
    <h1 class="logo">Masterclass Cooking Workshop</h1>
    <nav>
      <ul>
        <li>Home</li>
        <li>Courses</li>
        <li>Wishlist ({{ count }})</li>
      </ul>
    </nav>
  </header>
</template>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #333;
  color: white;
  padding: 15px 20px;
  border-radius: 8px;
}

.navbar ul {
  list-style: none;
  display: flex;
  gap: 20px;
  margin: 0;
  padding: 0;
}

.navbar a {
  color: white;
  text-decoration: none;
  font-weight: bold;
}

.logo {
  margin: 0;
}
</style>