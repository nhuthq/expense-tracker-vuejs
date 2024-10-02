<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="title">Text</label>
      <input
        id="title"
        type="text"
        v-model="name"
        placeholder="Enter text..."
      />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount<br />
        (negative - expense, positive - income)</label
      >
      <input
        id="amount"
        type="text"
        v-model="amount"
        placeholder="Enter amount..."
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref } from "vue";
import { useToast } from "vue-toast-notification";

const name = ref("");
const amount = ref("");
const toast = useToast();
const emit = defineEmits(["onSubmitTransaction"]);

const onSubmit = () => {
  if (!name.value || !amount.value) {
    toast.error("Both fields must be filled!");

    return;
  }

  const transactionData = {
    name: name.value,
    amount: parseFloat(amount.value),
  };

  emit("onSubmitTransaction", transactionData);

  name.value = "";
  amount.value = "";
};
</script>
