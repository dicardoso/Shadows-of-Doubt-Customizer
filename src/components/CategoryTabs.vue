<template>
  <v-container>
    <v-overlay :model-value="loading" class="align-center justify-center" persistent>
      <v-progress-circular indeterminate color="rgb(255, 0, 89)" size="64" />
    </v-overlay>
    <v-tabs v-model="tab" background-color="grey darken-4" dark>
      <v-tab border rounded slider-color="rgb(255, 0, 89)">
        {{ $t('categories.general') }}
      </v-tab>
      <v-tab
        v-for="category in categories"
        :key="category.name"
        border
        rounded
        slider-color="rgb(255, 0, 89)"
      >
        {{ $t(category.label) }}
      </v-tab>
    </v-tabs>

    <v-tabs-window v-model="tab" background-color="grey">
      <v-tabs-window-item class="mt-2">
        <general-tab :model-value="modelValue" />
      </v-tabs-window-item>
      <v-tabs-window-item class="mt-2">
        <citizen-tab :model-value="modelValue.citizens" />
      </v-tabs-window-item>
      <v-tabs-window-item class="mt-2">
        <street-tab :model-value="modelValue.streets" />
      </v-tabs-window-item>
      <v-tabs-window-item class="mt-2">
        <district-tab :model-value="modelValue.districts" />
      </v-tabs-window-item>
    </v-tabs-window>
  </v-container>
</template>

<script setup>
import { ref, reactive } from 'vue'
import GeneralTab from './tabs/GeneralTab.vue'
import CitizenTab from './tabs/CitizenTab.vue'
import StreetTab from './tabs/StreetTab.vue'
import DistrictTab from './tabs/DistrictTab.vue'

defineProps({
  modelValue: Object,
  loading: {
    type: Boolean,
    default: false,
  },
})

const tab = ref(0)

const categories = [
  { name: 'citizens', label: 'categories.citizens' },
  { name: 'streets', label: 'categories.streets' },
  { name: 'districts', label: 'categories.districts' },
]
</script>

<style scoped>
.neon-list {
  background-color: #1a1a1a;
  border: 1px solid rgb(255, 0, 89);
  padding: 10px;
}
</style>
