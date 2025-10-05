<template>
    <div>
        <h4>Income</h4>
        <p id="money-plus" class="money plus">+${{ ins }}</p>
    </div>
    <div>
        <h4>Expense</h4>
        <p id="money-minus" class="money minus">-${{ outs }}</p>
    </div>
</template>
<script setup>
import { defineProps } from 'vue';
const props = defineProps({
    ins: {
        type: Number,
        required: true
    },
    outs: {
        type: Number,
        required: true
    },
});
</script>