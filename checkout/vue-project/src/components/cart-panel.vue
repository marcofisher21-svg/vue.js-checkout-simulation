<template>
  <div class="cart-panel">
    <h2>Your Cart</h2>

    <div v-if="cart.length === 0">
      <p>Your cart is empty.</p>
    </div>

    <div v-else>
      <div 
        class="cart-item"
        v-for="item in cart" 
        :key="item.id"
      >
        <span>{{ item.title }}</span>

        <input 
          type="number" 
          min="1"
          v-model.number="item.qty"
          @change="$emit('updateQty', item.id, item.qty)"
        />

        <span>R{{ item.qty * item.price }}</span>

        <button @click="$emit('removeItem', item.id)">X</button>
      </div>

      <!-- SUMMARY -->
      <div class="summary">
        <p>Subtotal: R{{ subtotal }}</p>
        <p>Tax ({{ taxRate * 100 }}%): R{{ tax }}</p>
        <h3>Grand Total: R{{ total }}</h3>
      </div>

      <button class="clear" @click="$emit('clearCart')">
        Clear Cart
      </button>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue"

const props = defineProps({
  cart: Array,
  taxRate: Number
})

const subtotal = computed(() =>
  props.cart.reduce((sum, i) => sum + i.price * i.qty, 0)
)

const tax = computed(() => subtotal.value * props.taxRate)

const total = computed(() => subtotal.value + tax.value)
</script>

<style>
.cart-panel {
  background: #fff;
  padding: 20px;
  border-radius: 10px;
  width: 350px;
}
.cart-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 8px;
}
.clear {
  margin-top: 20px;
  width: 100%;
}
</style>
