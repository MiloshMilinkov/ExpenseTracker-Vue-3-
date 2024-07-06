<template>
  <Header />
  <div class="container">
    <Balance :total = "+total" />
    <IncomeExpenses :transactions = "transactions" />
    <TransactionLists :transactions = "transactions" />
    <AddTransactions @transaction-submited="addTransaction" />
  </div>
</template>

<script setup>
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import IncomeExpenses from './components/IncomeExpenses.vue';
  import TransactionLists from './components/TransactionLists.vue';
  import AddTransactions from './components/AddTransactions.vue';
  import { ref, computed } from 'vue';
  import { useToast } from 'vue-toastification';

  const toast = useToast();

  const transactions = ref ([ 
    {id: 1, text: 'Flower', amount: -19.99},
    {id: 2, text: 'Beer', amount: -4.99},
    {id: 3, text: 'Paycheck', amount: +540.00},
    {id: 4, text: 'Child Support', amount: -2000.00}
  ]);
    
  //Get total
  const total = computed(() => {
    return transactions.value.reduce((acc, transaction) =>{
      return acc + transaction.amount;
    }, 0);
  });


  //addTransaction
  const addTransaction = (transactionData) =>{
    transactions.value.push({
      id: generateUniqueId(),
      text: transactionData.text,
      amount: transactionData.amount
    });

    toast.success('Transaction added.')
  };

  //Generate id
  const generateUniqueId = () => {
    return Math.floor(Math.random() * 1000);
  }

</script>

