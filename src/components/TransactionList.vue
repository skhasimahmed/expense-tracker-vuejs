<script setup>
const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(["transactionDeleted"]);

const deleteTransaction = (id) => {
  emit("transactionDeleted", id);
};

// console.log(transactions.length);
</script>

<template>
  <h3>History</h3>

  <p v-if="transactions.length === 0">No transactions yet.</p>

  <ul id="list" class="list" v-if="transactions.length">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.text }} <span>₹{{ transaction.amount.toFixed(2) }}</span
      ><button class="delete-btn" @click="deleteTransaction(transaction.id)">
        x
      </button>
    </li>
  </ul>
</template>
