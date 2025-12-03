<template>
  <div class="course-list">
    <h2>Course Catalogue</h2>

    <div class="grid">
      <div v-for="c in courses" :key="c.id" class="card">

        <img :src="c.img" />

        <h3>{{ c.title }}</h3>
        <p>Chef: {{ c.chef }}</p>
        <p>Skill: {{ c.skill }}</p>
        <p>Price: R{{ c.price }}</p>

        <button 
          :disabled="!c.available"
          @click="$emit('addToCart', c)"
        >
          {{ c.available ? "Add to Cart" : "Sold Out" }}
        </button>

      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  courses: Array
})
</script>

<style>
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
  gap: 15px;
}
.card {
  background: white;
  padding: 15px;
  border-radius: 10px;
}
button[disabled] {
  background: #888;
}
</style>
