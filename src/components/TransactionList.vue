<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount > 0 ? 'plus' : 'minus'"
    >
      {{ transaction.text }} <span>{{ transaction.amount }}$</span
      ><button @click="onDeleteTransaction(transaction.id)" class="delete-btn">
        x
      </button>
    </li>
  </ul>
</template>

<!-- <script>
export default {
  //Cách 1: dùng options API
  // data() {
  //   return {
  //     transactions: [
  //       { id: 1, text: "Flower", amount: 20 },
  //       { id: 2, text: "Book", amount: -400 },
  //       { id: 3, text: "Computer", amount: 800 },
  //       { id: 4, text: "Smart phone", amount: -200 },
  //     ],
  //   };
  // },

  //Cách 2: Viết trong hàm setup, rồi return ra là dùng
  setup() {
    const transactions = [
      { id: 1, text: "Flower", amount: 20 },
      { id: 2, text: "Book", amount: -400 },
      { id: 3, text: "Computer", amount: 800 },
      { id: 4, text: "Smart phone", amount: -200 },
    ];

    return {
      transactions,
    };
  },
};
</script> -->

<!-- Cách 3: Trong thẻ scrip thêm setup keyword, và k cần return -->
<!-- <script setup>
const transactions = [
  { id: 1, text: "Flower", amount: 20 },
  { id: 2, text: "Book", amount: -400 },
  { id: 3, text: "Computer", amount: 800 },
  { id: 4, text: "Smart phone", amount: -200 },
];
</script> -->

<script setup>
const props = defineProps({
  transactions: {
    type: Array,
    require: true,
  },
});
const emit = defineEmits(["deleteTransaction"]);

const onDeleteTransaction = (transactionId) => {
  emit("deleteTransaction", transactionId);
};
</script>
