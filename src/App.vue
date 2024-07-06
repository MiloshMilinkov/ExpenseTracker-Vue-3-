<template>
  <Header />
  <div class="container">
    <Balance />
    <IncomeExpenses/>
    <TransactionLists :transactions = "transactions" />
    <AddTransactions/>
  </div>
</template>

<script setup>
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import IncomeExpenses from './components/IncomeExpenses.vue';
  import TransactionLists from './components/TransactionLists.vue';
  import AddTransactions from './components/AddTransactions.vue';
  import { ref } from 'vue';

  const transactions = ref ([ 
    {id: 1, text: 'Flower', amount: -19.99},
    {id: 2, text: 'Beer', amount: -4.99},
    {id: 3, text: 'Paycheck', amount: +540.00}
  ]);
    

</script>

<style scoped>

</style>