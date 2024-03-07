<template>
  <Header />
  <div class="container">
    <Balance :total="+total" />
    <IncomeExpense :income="+income" :expense="+expense" />
    <TransactionList
      :transactions="transactions"
      @deleteTransaction="deleteTransaction"
    />
    <AddTransaction @addNewTransaction="addNewTransaction" />
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";
import { computed, ref } from "vue";

const transactions = ref([
  { id: 1, text: "Flower", amount: 20 },
  { id: 2, text: "Book", amount: -400 },
  { id: 3, text: "Computer", amount: 800 },
  { id: 4, text: "Smart phone", amount: -2000 },
]);

const total = computed(() => {
  return transactions.value.reduce((acc, trans) => acc + trans.amount, 0);
});

const income = computed(() => {
  return transactions.value
    .filter((trans) => trans.amount > 0)
    .reduce((acc, trans) => acc + trans.amount, 0);
});

const expense = computed(() => {
  return transactions.value
    .filter((trans) => trans.amount < 0)
    .reduce((acc, trans) => acc + trans.amount, 0);
});

const addNewTransaction = (transaction) => {
  const newTrans = {
    id: generateRandomId(),
    text: transaction.text,
    amount: parseFloat(transaction.amount),
  };
  transactions.value.push(newTrans);
};

const deleteTransaction = (transactionId) => {
  transactions.value = transactions.value.filter(
    (trans) => trans.id !== transactionId
  );
};

const generateRandomId = () => {
  return Math.floor(Math.random() * 100000);
};
</script>

<style scoped></style>
