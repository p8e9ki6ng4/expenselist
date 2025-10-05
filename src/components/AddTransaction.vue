<template>
    <h3>Add new transaction</h3>
    <form id="form" @submit.prevent="going">
        <div class="form-control">
        <label for="text">Text</label>
        <input type="text" id="text" placeholder="Enter text..." 
        v-model="text"/>
        </div>
        <div class="form-control">
        <label for="amount">Amount <br />
        (negative - expense, positive - income)</label>
        <input type="number" id="amount" placeholder="Enter amount..." 
        v-model="amount"/>
        </div>
        <button class="btn">Add transaction</button>
    </form>
</template>
<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification';
const emit=defineEmits(['trans'])
const text = ref(''), amount = ref('');
const toast = useToast();
const going = () => {
    if (!text.value || !amount.value) {
        toast.error("Both fields must be filled");
        return;
    }
    // console.log(text.value, amount.value);
    const transdate = {
        text:text.value,amount:parseFloat(amount.value)
    }
    emit('trans', transdate);
    text.value = '', amount.value = '';
}
</script>