<template>
  <div class="card">
    <h2>{{ title }}</h2>
    <div v-for="(item, index) in modelValue" :key="index" class="input-group">
      <input
        v-model="modelValue[index]"
        class="input"
        type="text"
        :placeholder="`Nome ${index + 1}`"
      />
    </div>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  modelValue: Array,
})

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
