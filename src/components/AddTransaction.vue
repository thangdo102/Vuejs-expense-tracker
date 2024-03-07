<template>
  <h3>Add new transaction</h3>
  <form @submit.prevent="submitForm" id="form">
    <div class="form-control">
      <label for="text">Text</label>
      <input v-model="text" type="text" id="text" placeholder="Enter text..." />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input
        v-model="amount"
        type="string"
        id="amount"
        placeholder="Enter amount..."
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref, defineProps } from "vue";

const text = ref("");
const amount = ref("");

const props = defineProps({});

const emit = defineEmits(["addNewTransaction"]);

const submitForm = () => {
  if (!text.value || !amount.value) return;

  const transaction = {
    text: text.value,
    amount: amount.value,
  };

  emit("addNewTransaction", transaction);
};
</script>
