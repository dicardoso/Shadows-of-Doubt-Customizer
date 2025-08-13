<template>
  <v-card class="neon-list">
    <v-list>
      <v-list-item v-for="(item, index) in modelValue" :key="index">
        <v-row class="d-flex my-2 mx-2 ga-2 align-center">
          <span>{{ index + 1 }}</span>
          <v-text-field
            v-model="item.name"
            :label="$t('tab.streets.name')"
            dense
            hide-details
            variant="outlined"
          />
          <v-text-field
            v-model="item.streetSuffix"
            :label="$t('tab.streets.street-suffix')"
            dense
            hide-details
            variant="outlined"
          />
          <v-text-field
            v-model="item.designStyle"
            disabled
            :label="$t('tab.streets.design-style')"
            dense
            hide-details
            variant="outlined"
          />
        </v-row>
      </v-list-item>
    </v-list>
  </v-card>
</template>
<script setup>
defineProps({
  modelValue: Object,
})
</script>
