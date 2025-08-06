<template>
  <div class="card">
    <div>
      <span>citizenName: </span>
      <input v-model="modelValue.citizenName"></input>
    </div>
    <div>
      <span>firstName: </span>
      <input v-model="modelValue.firstName"></input>
    </div>
    <div>
      <span>surName: </span>
      <input v-model="modelValue.surName"></input>
    </div>
    <!-- <div v-for="(item, index) in modelValue" :key="index" class="input-group">
      {{ item }}
    </div> -->
  </div>
</template>

<script setup>
defineProps({
  modelValue: Object,
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
