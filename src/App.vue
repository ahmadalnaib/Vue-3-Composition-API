<template>
 <Header />
 <div class="container">
  <Balance :total="total"/>
  <IncomeExpense :income="+income" :expense="+expense"/>
  <TransactionList :transactions="transactions"/>
  <AddTransaction />

 </div>
</template>



<script setup>
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpense from './components/IncomeExpense.vue'
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue'
import {ref,computed} from 'vue'


const transactions = ref([
  { id: 1, text: 'Flower', amount: -20 },
  { id: 2, text: 'Salary', amount: 300 },
  { id: 3, text: 'Book', amount: -10 },
  { id: 4, text: 'Camera', amount: 150.20 }
]);

// get total

const total=computed(()=>{
  return transactions.value
  .reduce((acc,item)=>(acc+=item.amount),0)
  .toFixed(2)
})



// get income
const income=computed(()=>{
  return transactions.value
  .filter(item=>item.amount > 0 )
  .reduce((acc,item)=>(acc+=item.amount),0)
  .toFixed(2)
})




//get expense

const expense=computed(()=>{
  return transactions.value
  .filter(item=>item.amount < 0 )
  .reduce((acc,item)=>(acc+=item.amount),0)
  .toFixed(2)
})

</script>