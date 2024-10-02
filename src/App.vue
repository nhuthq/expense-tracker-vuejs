<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpense :income="+income" :expenses="+expenses" />
    <TransactionList :transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<script setup>
import { ref } from "vue";
import { computed } from "vue";
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import AddTransaction from "./components/AddTransaction.vue";
import TransactionList from "./components/TransactionList.vue";

const transactions = ref([
  { id: 1, name: "Americano", amount: -5.0 },
  { id: 2, name: "Breakfast", amount: -3.99 },
  { id: 3, name: "Salary", amount: 1000.0 },
  { id: 4, name: "Lunch", amount: -4.99 },
  { id: 5, name: "Book", amount: -2.0 },
  { id: 5, name: "Coffee", amount: -5.0 },
  { id: 6, name: "Course", amount: 50.0 },
]);

// Get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});

// Get income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

// Get expense
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + -transaction.amount;
    }, 0)
    .toFixed(2);
});
</script>
