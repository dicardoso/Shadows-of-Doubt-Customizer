<template>
  <v-card class="neon-list">
    <v-list>
      <v-list-item v-for="(item, index) in modelValue" :key="index">
        <v-row class="d-flex my-2 mx-2 ga-2 align-center">
          <span>{{ index + 1 }}</span>
          <v-text-field
            v-model="item.name"
            :label="$t('tab.districts.name')"
            dense
            hide-details
            variant="outlined"
          />
          <v-select
            v-model="item.preset"
            :label="$t('tab.districts.preset')"
            :items="presetList"
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
const props = defineProps({
  modelValue: Object,
})
const presetList = ref()

onMounted(() => {
  presetList.value = props.modelValue
    ? Array.from(new Set(props.modelValue.map((item) => item.preset))).sort((a, b) =>
        a.localeCompare(b),
      )
    : []
})
</script>
