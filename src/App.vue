<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpense :income="+income" :expenses="+expenses" />
    <TransactionList
      :transactions="transactions"
      @onDeleteTransaction="handleDeleteTransaction"
    />
    <AddTransaction @onSubmitTransaction="handleSubmitTransaction" />
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { computed } from "vue";
import { useToast } from "vue-toast-notification";
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";

import IncomeExpense from "./components/IncomeExpense.vue";
import AddTransaction from "./components/AddTransaction.vue";
import TransactionList from "./components/TransactionList.vue";

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));
  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

const toast = useToast();

const transactions = ref([]);

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

const handleSubmitTransaction = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId,
    name: transactionData.name,
    amount: transactionData.amount,
  });

  saveTransactionsToLocal();

  toast.success("Transaction add successfully!");
};

const handleDeleteTransaction = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );
  saveTransactionsToLocal();
  toast.success("Transaction delete successfully!");
};

const generateUniqueId = () => {
  return Math.floor(Math.random() * 10000000);
};

const saveTransactionsToLocal = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};
</script>
