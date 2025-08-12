<template>
    <div>
        <v-list class="neon-list">
            <EditableListItem v-for="(item, index) in filteredItems" :key="index" :value="item"
                @input="updateItem(index, $event)" />
        </v-list>
    </div>
</template>

<script setup>
import { computed, ref, watch } from 'vue'
import EditableListItem from './EditableListItem.vue'

const props = defineProps({
    categoryName: String,
    items: Array,
    search: String
})
const emit = defineEmits(['update-items', 'update:search'])

const localSearch = ref(props.search)

watch(localSearch, val => {
    emit('update:search', val)
})

const filteredItems = computed(() =>
    props.items.filter(item =>
        item.toLowerCase().includes(localSearch.value.toLowerCase())
    )
)

function updateItem(index, newValue) {
    const updated = [...props.items]
    updated[index] = newValue
    emit('update-items', updated)
}
</script>

<style scoped>
.neon-list {
    background-color: #1a1a1a;
    border: 1px solid #0ff;
    padding: 10px;
}
</style>