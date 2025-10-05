<template>
    <h4>Your Balance</h4>
    <h1 id="balance">${{tot}}</h1>
</template>
<script setup>
import { defineProps } from 'vue';
const props = defineProps({
    tot: {
        type: Number,
        required:true,
    },
});
</script>