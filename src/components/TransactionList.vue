<script setup>
    import { defineProps } from 'vue';
    const props = defineProps({
        transactions: {
            type: Array,
            required: true,
        }
    })
</script>

<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li v-for="trasaction in transactions" :key="trasaction.id" :class="trasaction.amount < 0 ? 'minus' : 'plus'">
            {{ trasaction.text }} <span>${{ trasaction.amount }}</span><button class="delete-btn">x</button>
        </li>
    </ul>
</template>