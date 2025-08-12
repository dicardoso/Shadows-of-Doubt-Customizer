<template>
    <v-container>
        <v-tabs v-model="tab" background-color="grey darken-4" dark>
            <v-tab v-for="category in categories" :key="category.name" border rounded slider-color="rgb(255, 0, 89)">
                {{ $t(category.label) }}
            </v-tab>
        </v-tabs>

        <v-tabs-window v-model="tab" background-color="grey">
            <v-tabs-window-item v-for="(category, idx) in categories" :key="category.name" class="mt-2">
                <v-list class="neon-list">
                    <v-list-item v-for="(item, index) in filteredItems(category.name)" :key="index">
                        <v-text-field v-model="editedData[category.name][index]" dense hide-details
                            variant="outlined" />
                    </v-list-item>
                </v-list>
            </v-tabs-window-item>
        </v-tabs-window>
    </v-container>
</template>

<script setup>
import { ref, reactive } from 'vue'
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

const tab = ref(0)

const categories = [
    { name: 'characters', label: 'categories.characters' },
    { name: 'streets', label: 'categories.streets' },
    { name: 'companies', label: 'categories.companies' }
]

const search = reactive({
    characters: '',
    streets: '',
    companies: ''
})

const editedData = reactive({
    characters: ['Alice', 'Bob', 'Charlie'],
    streets: ['Rua Azul', 'Avenida Central'],
    companies: ['CorpX', 'MegaCorp']
})

function filteredItems(category) {
    const term = search[category].toLowerCase()
    return editedData[category].filter(item =>
        item.toLowerCase().includes(term)
    )
}
</script>

<style scoped>
.neon-list {
    background-color: #1a1a1a;
    border: 1px solid rgb(255, 0, 89);
    padding: 10px;
}
</style>