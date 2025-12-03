<template>
  <div class="app">

    <HeaderBar :count="cartCount" />

    <div class="layout">

      <CourseList 
        :courses="courses"
        @addToCart="addToCart"
      />

      <!-- FIXED: correct PascalCase tag -->
      <CartPanel
        :cart="cart"
        :taxRate="taxRate"
        @updateQty="updateQty"
        @removeItem="removeItem"
        @clearCart="clearCart"
      />

    </div>

  </div>
</template>

<script setup>
import { ref, computed } from "vue"

// FIXED: corrected folder spelling
import CourseList from "./components/course-list.vue"
import CartPanel from "./components/cart-panel.vue"


const taxRate = 0.15  // 15% simple tax

// ---------------------------
// COURSE DATA (unchanged)
// ---------------------------
const courses = ref([
  { id: 1, title: "Italian Pasta Mastery", chef: "Marco Rossi", price: 219, skill: "Beginner", available: true, img: "https://i.postimg.cc/wTFCZSKq/images-q-tbn-ANd9Gc-Qc-Ad1V0f-VA3791Bi-JL1xl-VFOB5VX4h-XLJn-VQ-s.jpg" },
  { id: 2, title: "Advanced Sushi Art", chef: "Yuki Tanaka", price: 400, skill: "Expert", available: false, img: "https://i.postimg.cc/BvT6sXdd/images-q-tbn-ANd9Gc-Qo-XYm-FFQrhb-Wt1oo-Lzvy-Vle-Wv-Bhcr1Om-Q3Ag-s.jpg" },
  { id: 3, title: "French Pastry Basics", chef: "Lyon Sin-clair", price: 329, skill: "Intermediate", available: true, img: "https://i.postimg.cc/pXd8YFR0/images-q-tbn-ANd9Gc-TYb5dx-SEc61hz-LDmm-C6yac-MKVVba-X87VR509Y-Ejpkbpem45t-Zc-Aun-LI-s.jpg" },
  { id: 4, title: "Advanced Dessert Art", chef: "James Ford", price: 429, skill: "Expert", available: true, img: "https://i.postimg.cc/50bBvKPd/images-q-tbn-ANd9Gc-S7X0k-H-bjr-KN3u-VW-e-Barv-Cdb-Ldyzp-Sj3r-Tw-s.jpg" },
  { id: 5, title: "Chinese Cuisine Mastery", chef: "Xiao Li", price: 359, skill: "Intermediate", available: false, img: "https://i.postimg.cc/pV89xJk5/images-q-tbn-ANd9Gc-RL13TCD3c-Z98n-URe-Aw-L4PVHczru-VSy1Wsmjw-s.jpg" },
  { id: 6, title: "German Cuisine Mastery", chef: "Hans Müller", price: 259, skill: "Beginner", available: true, img: "https://i.postimg.cc/GpwwczR1/images-q-tbn-ANd9Gc-Ru2eg3h-L49A2456b-OFhk-Nx-I6wzso-WDFb01zg-s.jpg" }
])

// ---------------------------
// CART STATE
// ---------------------------
const cart = ref([])

// CART COUNT (for header)
const cartCount = computed(() =>
  cart.value.reduce((sum, item) => sum + item.qty, 0)
)

// ---------------------------
// CART ACTIONS
// ---------------------------

function addToCart(course) {
  if (!course.available) return

  const found = cart.value.find(item => item.id === course.id)

  if (found) {
    found.qty++
  } else {
    cart.value.push({ ...course, qty: 1 })
  }
}

function updateQty(id, qty) {
  const item = cart.value.find(i => i.id === id)
  if (!item) return

  if (qty <= 0) {
    cart.value = cart.value.filter(i => i.id !== id)
  } else {
    item.qty = qty
  }
}

function removeItem(id) {
  cart.value = cart.value.filter(i => i.id !== id)
}

function clearCart() {
  cart.value = []
}

</script>

<style>
.app {
  padding: 20px;
  font-family: Arial, sans-serif;
}

.layout {
  display: flex;
  gap: 20px;
}

@media(max-width: 800px) {
  .layout {
    flex-direction: column;
  }
}

body {
  background: linear-gradient(
    90deg,
    rgba(194,133,35,1) 0%,
    rgba(76,156,47,1) 50%,
    rgba(237,83,83,1) 100%
  );
}
</style>
