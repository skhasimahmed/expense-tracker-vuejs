<script setup>
const props = defineProps({
  total: {
    type: Number,
    required: true,
  },
});
</script>

<template>
  <h4>Your Balance</h4>
  <h1 id="balance">₹{{ total.toFixed(2) }}</h1>
</template>
