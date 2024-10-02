<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount >= 0 ? 'plus' : 'minus'"
    >
      {{ transaction.name }} <span>$ {{ transaction.amount }}</span
      ><button @click="onDelete(transaction.id)" class="delete-btn">x</button>
    </li>
  </ul>
</template>

<script setup>
import { defineProps } from "vue";

const emit = defineEmits(["onDeleteTransaction"]);

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const onDelete = (id) => {
  emit("onDeleteTransaction", id);
};
</script>
