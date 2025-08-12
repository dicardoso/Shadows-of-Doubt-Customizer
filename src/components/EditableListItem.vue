<template>
    <v-list-item>
        <v-text-field v-model="localValue" hide-details variant="outlined" @input="$emit('input', localValue)" />
    </v-list-item>
</template>

<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
    value: String
})

const localValue = ref(props.value)

watch(() => props.value, val => {
    localValue.value = val
})
</script>