<template>
  <h3>Add new transaction</h3>
  <form>
    <div class="form-control">
      <label for="title">Text</label>
      <input id="title" type="text" placeholder="Enter text..." />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount<br />
        (negative - expense, positive - income)</label
      >
      <input id="amount" type="number" placeholder="Enter amount..." />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>
