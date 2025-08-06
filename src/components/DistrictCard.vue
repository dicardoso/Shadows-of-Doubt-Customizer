<template>
  <div class="card">
    <div>
      <span>name: </span>
      <input v-model="modelValue.name"></input>
    </div>
    <div>
      <span>preset: </span>
      <select v-model="modelValue.preset">
        <option v-for="option in items" :value="option.value">
          {{ option.label }}
        </option>
      </select>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
defineProps({
  modelValue: Object,
})
const items = ref([
  { label: 'CBD', value: 'CBD' },
  { label: 'Chinatown', value: 'Chinatown' },
  { label: 'Industrial', value: 'Industrial' },
  { label: 'RedLight', value: 'RedLight' },
  { label: 'Residential', value: 'Residential' },
]);

defineEmits(['update:modelValue'])
</script>

<style scoped>
.card {
  background-color: #222;
  border: 1px solid #444;
  padding: 1rem;
  margin-bottom: 1rem;
  border-radius: 8px;
  color: #fff;
  gap: 10px;
}
.input-group {
  margin: 0.3rem 0;
}
.input {
  width: 100%;
  padding: 0.5rem;
  background-color: #333;
  color: #fff;
  border: 1px solid #555;
  border-radius: 4px;
}
</style>
