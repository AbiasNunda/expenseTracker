<script setup>
  import Header from "./components/Header.vue";
  import Balance from "./components/Balance.vue";
  import IncomeExpense from "./components/IncomeExpenses.vue";
  import Transactions from "./components/TransactionList.vue";
  import AddTransaction from "./components/AddTransaction.vue";
  import { ref, computed } from 'vue';
  import { useToast } from 'vue-toastification';
  const toast  = useToast()

  const transactions = ref([
    { id: 1, text: 'Flower', amount: -19.99 },
    { id: 2, text: 'Salary', amount: 200.99 },
    { id: 3, text: 'Blook', amount: -19 },
    { id: 4, text: 'Camera', amount: 150 },
  ])

  // GET BALANCE
  const total = computed(()=> {
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount; 
    }, 0)
  })

// GET INCOME
const income = computed(()=> {
  return transactions.value
  .filter((transaction)=> transaction.amount > 0)
  .reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0)
  .toFixed(2)
})

// GET EXPEMSES
const expenses = computed(()=> {
  return transactions.value
  .filter((transaction)=> transaction.amount < 0)
  .reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0)
  .toFixed(2)
})

// ADD TRANSACTION
const handletransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount
  })
  toast.success('Trasaction Added!')
}
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000)
}
</script>

<template>
  <Header />
  <div class="container">
    <Balance :total="+total" />
    <IncomeExpense :income="+income" :expenses="+expenses" />
    <Transactions :transactions ="transactions" />
    <AddTransaction @transactionSubmitted="handletransactionSubmitted" />
  </div>
</template>


