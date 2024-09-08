<script setup>
import moment from "moment";

const props = defineProps({
  transaction: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(["transactionDeleted"]);

const deleteTransaction = () => {
  emit("transactionDeleted", props.transaction.id);
};

const checkCharacters = (str) => {
  const max = 25;
  return str.length > max ? str.substring(0, max) + "..." : str;
};
</script>

<template>
  <li :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus'">
    <div
      class="ribbon"
      :class="props.transaction.amount > 0 ? 'ribbon-credit' : 'ribbon-debit'"
    >
      {{ props.transaction.amount > 0 ? "Credit" : "Debit" }}
    </div>

    <div>
      <p style="margin: 0px" :title="transaction.text">
        {{ checkCharacters(transaction.text) }}
      </p>
      <span
        style="
          font-size: 11px;
          font-style: italic;
          font-weight: 500;
          color: gray;
        "
        >{{ moment(transaction.date).fromNow() }}</span
      >
    </div>

    <div style="display: flex; align-items: center">
      <p>₹{{ Math.abs(transaction.amount).toFixed(2) }}</p>
    </div>
    <button class="delete-btn" @click="deleteTransaction">x</button>
  </li>
</template>
