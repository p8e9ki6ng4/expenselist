<template>
  <title>Expense Tracker</title>
  <Header />
  <div class="container">
    <Balance :tot="tot"/>
    <div class="inc-exp-container">
      <IncomeExpenses :ins="+ins" :outs="+outs"/>
    </div>
    <TransactionList :dk="gcd" @tdel="handledel"/>
    <AddTransaction @trans="handleadd"/>
  </div>
  
</template>
<script setup>
import { computed, onMounted, ref } from 'vue';
import { useToast } from 'vue-toastification';
import AddTransaction from './components/AddTransaction.vue';
import Balance from './components/Balance.vue';
import Header from './components/Header.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
const toast = useToast();
const gcd=ref([
  // { id: 1, text: "mzd", amount: -8964 },
  // { id: 2, text: "dxp", amount: -8964 },
  // { id: 3, text: "hyb", amount: 89 },
  // { id: 4, text: "zzy", amount: 64 },
  // { id: 5, text: "jzm", amount: -8964 },
  // { id: 6, text: "hjt", amount: -8964 },
  // { id: 7, text: "xjp", amount: -8964 },
  // {id:8,text:"lyh",amount:198964}
])
const tot = computed(() => {
  return gcd.value.reduce((acceed, ccb) => {
    return acceed + ccb.amount;
  },0);
});
const ins = computed(() => {
  return gcd.value
  .filter(p=>p.amount>0).reduce((acceed, ccb) => {
    return acceed + ccb.amount;
  },0).toFixed(2);
});
const outs = computed(() => {
  return gcd.value
  .filter(p=>p.amount<0).reduce((acceed, ccb) => {
    return acceed + ccb.amount;
  },0).toFixed(2)*(-1);
});
// console.log(gcd.value.filter(p=>p.amount>0))
// console.log(gcd.value.filter(p=>p.amount<0))
const handleadd = (transdata) => {
  // console.log(transdata);
  gcd.value.push({
    id: uid(),
    text: transdata.text,
    amount:transdata.amount
  });
  savetoloc();
  // console.log(uid());
  toast.success('Transaction added')
  
};
const uid = () => {
  return Math.floor(Math.random()*1000000);
}
const handledel = (id) => {
  gcd.value = gcd.value.filter((k) => k.id != id);
  savetoloc();
  toast.success('Transaction deleted')
};
onMounted(() => {
  const savet = JSON.parse(localStorage.getItem('gcd'));
  if (savet) {
    gcd.value = savet;
  }
});
const savetoloc = () => {
  localStorage.setItem('gcd',JSON.stringify(gcd.value))
}
</script>
<style scoped>

</style>
