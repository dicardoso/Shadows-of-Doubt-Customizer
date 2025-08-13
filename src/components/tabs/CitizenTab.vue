<template>
  <v-card class="neon-list">
    <v-list>
      <v-lazy v-for="(item, index) in modelValue" :key="index" min-height="60">
        <v-list-item>
          <v-row class="d-flex my-2 mx-2 ga-2 align-center">
            <span>{{ index + 1 }}</span>
            <v-text-field
              v-model="item.citizenName"
              :label="$t('tab.citizens.name')"
              dense
              hide-details
              variant="outlined"
            />
            <v-text-field
              v-model="item.firstName"
              :label="$t('tab.citizens.first-name')"
              dense
              hide-details
              variant="outlined"
            />
            <v-text-field
              v-model="item.surName"
              :label="$t('tab.citizens.sur-name')"
              dense
              hide-details
              variant="outlined"
            />
            <v-text-field
              v-model="item.casualName"
              :label="$t('tab.citizens.casual-name')"
              dense
              hide-details
              variant="outlined"
            />
          </v-row>
        </v-list-item>
      </v-lazy>
    </v-list>
  </v-card>
</template>

<script setup>
defineProps({
  modelValue: {
    type: Array,
    required: true,
  },
})
</script>
