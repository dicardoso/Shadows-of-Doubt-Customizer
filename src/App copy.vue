<template>
  <div class="app-container">
    <h1>Editor de Arquivo .cit</h1>

    <input type="file" accept=".cit,.json" @change="onFileChange" />

    <div v-if="cityData" class="editor">
      <h2>Editar dados da cidade</h2>
      <div v-for="(items, group) in cityData" :key="group" class="group-section">
        <h3>{{ group }}</h3>

        <div v-if="Array.isArray(items)">
          <div v-for="(item, index) in items" :key="index" class="item-edit">
            <h4>{{ group }} #{{ index + 1 }}</h4>
            <div v-for="(value, key) in item" :key="key" class="field-edit">
              <label :for="group + '-' + index + '-' + key">{{ key }}</label>
              <input
                :id="group + '-' + index + '-' + key"
                v-model="cityData[group][index][key]"
                :type="inputType(value)"
              />
            </div>
          </div>
        </div>

        <div v-else-if="typeof items === 'object' && items !== null">
          <div v-for="(value, key) in items" :key="key" class="field-edit">
            <label :for="group + '-' + key">{{ key }}</label>
            <input
              :id="group + '-' + key"
              v-model="cityData[group][key]"
              :type="inputType(value)"
            />
          </div>
        </div>

        <div v-else>
          <p>Tipo de dado não suportado para edição</p>
        </div>
      </div>

      <button @click="downloadCit">Baixar arquivo modificado</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const cityData = ref(null);

function onFileChange(event) {
  const file = event.target.files[0];
  if (!file) return;
  
  const reader = new FileReader();
  reader.onload = e => {
    try {
      let aux = JSON.parse(e.target.result);
      cityData.value = {
        build: aux.build, 
        citizens: aux.citizens, 
        cityName: aux.cityName, 
        cityTiles: aux.cityTiles, 
        district: aux.districts,
        streets: aux.streets
      };
      console.log('Dados carregados:', cityData.value);
    } catch (err) {
      alert('Arquivo inválido ou não é JSON.');
    }
  };
  reader.readAsText(file);
}

function inputType(value) {
  if (typeof value === 'number') return 'number';
  if (typeof value === 'boolean') return 'checkbox';
  return 'text';
}

function downloadCit() {
  if (!cityData.value) return;

  const jsonStr = JSON.stringify(cityData.value, null, 2);
  const blob = new Blob([jsonStr], { type: 'application/json' });
  const url = URL.createObjectURL(blob);

  const a = document.createElement('a');
  a.href = url;
  a.download = 'city_modified.cit';
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);

  URL.revokeObjectURL(url);
}
</script>

<style>
.app-container {
  font-family: Arial, sans-serif;
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
}
.group-section {
  margin-top: 30px;
  border-top: 1px solid #ddd;
  padding-top: 15px;
}
.item-edit {
  margin-bottom: 20px;
  padding: 10px;
  background: #f9f9f9;
  border-radius: 6px;
}
.field-edit {
  margin-bottom: 8px;
}
label {
  display: inline-block;
  width: 120px;
  font-weight: bold;
}
input[type='text'],
input[type='number'] {
  width: 300px;
  padding: 4px 6px;
  font-size: 14px;
}
input[type='checkbox'] {
  transform: scale(1.2);
}
button {
  margin-top: 20px;
  padding: 10px 15px;
  font-size: 16px;
  cursor: pointer;
}
</style>
