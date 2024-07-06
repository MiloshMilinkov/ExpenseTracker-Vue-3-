<template>
  <Header />
  <div class="container">
    <Balance :total = "+total" />
    <IncomeExpenses :transactions = "transactions" />
    <TransactionLists :transactions = "transactions" @transactionDeleted="deleteTransaction" />
    <AddTransactions @transaction-submited="addTransaction" />
  </div>
</template>

<script setup>
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import IncomeExpenses from './components/IncomeExpenses.vue';
  import TransactionLists from './components/TransactionLists.vue';
  import AddTransactions from './components/AddTransactions.vue';
  import { ref, computed, onMounted } from 'vue';
  import { useToast } from 'vue-toastification';

  const toast = useToast();

  const transactions = ref ([]);
    
  onMounted(() => {
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

    if(savedTransactions){
      transactions.value = savedTransactions;
    }
  });
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
    saveTransactionsToLocalStorage();

    toast.success('Transaction added.')
  };

  //Generate id
  const generateUniqueId = () => {
    return Math.floor(Math.random() * 1000);
  };

  const deleteTransaction = (id) =>{
    transactions.value = transactions.value.filter(transaction => transaction.id !== id);
    saveTransactionsToLocalStorage();

    toast.success('Transaction removed');
  }

  //Save to localStorage
  const saveTransactionsToLocalStorage = () => {
    localStorage.setItem('transactions', JSON.stringify(transactions.value));
  }

</script>

