<template>
<div class="inc-exp-container">
    <div>
        <h4>Income</h4>
        <p id="money-plus" class="money plus">+ ${{ income }}</p>
    </div>
    <div>
        <h4>Expense</h4>
        <p id="money-minus" class="money minus">${{ expense }}</p>
    </div>
</div>
</template>


<script setup>
  import { ref, computed } from 'vue';
    const props = defineProps({
        transactions: {
            type: Array,
            required: true
        },
    });

    //Get income
    const income = computed(() => {
    return props.transactions
      .filter(transaction => transaction.amount > 0)
      .reduce((acc, transaction) =>{
      return acc + transaction.amount;
    }, 0).toFixed(2);
  })


  //Get expenses
  const expense = computed(() => {
    return props.transactions
      .filter(transaction => transaction.amount < 0)
      .reduce((acc, transaction) =>{
      return acc + transaction.amount;
    }, 0).toFixed(2);
  })
 

</script>


