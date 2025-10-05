<template>
<h3>History</h3>
<ul id="list" class="list">
    <li v-for="t in dk"
    :key="t.id"
    :class="t.amount<0?'minus':'plus'">
        {{ t.text }}
        <span>${{ t.amount }}</span>
        <button @click="del(t.id)" class="delete-btn">x</button>
    </li>
</ul>
</template>
<script setup>
import { defineProps } from 'vue';
const emit=defineEmits(['tdel'])
const dd = defineProps({
    dk: {
        type: Array,
        required: true,
    },
});
const del = (id) => {
    emit('tdel', id)
};
</script>