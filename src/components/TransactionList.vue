<script setup>
import Transaction from "./Transaction.vue";

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(["transactionDeleted"]);

const handleTransactionDeleted = (id) => {
  emit("transactionDeleted", id);
};
</script>

<template>
  <h3>History</h3>

  <p v-if="transactions.length === 0">No transactions yet.</p>

  <ul id="list" class="list" v-if="transactions.length">
    <Transaction
      :key="transaction.id"
      v-for="transaction in transactions"
      :transaction="transaction"
      @transactionDeleted="handleTransactionDeleted"
    />
  </ul>
</template>
