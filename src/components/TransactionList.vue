<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount >= 0 ? 'plus' : 'minus'"
    >
      {{ transaction.name }} <span>$ {{ transaction.amount }}</span
      ><button class="delete-btn">x</button>
    </li>
  </ul>
</template>

<script setup>
import { ref } from "vue";

const transactions = ref([
  { id: 1, name: "Americano", amount: -5.0 },
  { id: 1, name: "Breakfast", amount: -3.99 },
  { id: 1, name: "Salary", amount: 1000.0 },
  { id: 1, name: "Lunch", amount: -4.99 },
  { id: 1, name: "Book", amount: -2.0 },
  { id: 1, name: "Course", amount: 50.0 },
]);
</script>
