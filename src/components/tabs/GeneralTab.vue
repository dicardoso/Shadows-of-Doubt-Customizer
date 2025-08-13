<template>
  <v-card class="neon-list">
    <v-row class="my-2 mx-2 ga-2">
      <v-text-field
        v-model="modelValue.cityName"
        variant="outlined"
        :label="$t('tab.general.city-name')"
      />
    </v-row>
    <v-row class="my-2 mx-2 ga-2">
      <v-text-field
        v-model="modelValue.population"
        disabled
        variant="outlined"
        :label="$t('tab.general.population')"
      />
      <v-text-field
        :model-value="
          modelValue.citySize ? `${modelValue.citySize.x} x ${modelValue.citySize.y}` : null
        "
        disabled
        variant="outlined"
        :label="$t('tab.general.city-size')"
      />
      <v-text-field
        v-model="modelValue.build"
        disabled
        variant="outlined"
        :label="$t('tab.general.build')"
      />
      <v-text-field
        v-model="modelValue.seed"
        disabled
        variant="outlined"
        :label="$t('tab.general.seed')"
      />
    </v-row>
  </v-card>
</template>
<script setup>
defineProps({
  modelValue: Object,
})
</script>
