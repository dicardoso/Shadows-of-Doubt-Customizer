<template>
  <div class="container">
    <h1>Personalizador Shadows of Doubt</h1>

    <input type="file" accept=".cit,.json" @change="handleFile" />
    <div class="general-info">
      {{ $t('test.new') }}
      <div>{{data.cityName}}</div>
      <div>{{data.build}}</div>
    
    <button v-if="fileName" @click="downloadFile">Baixar Arquivo Modificado</button>
    </div>
    <div v-if="Object.keys(data).length" class="editor">
      <div class="card">
        <h2>Citizens</h2>
        <div v-for="value in data['citizens']" :key="value.id" class="citizen-card">  
          <citizen-card
            :modelValue="value"
          />
        </div>
      </div>
      <div class="card">
        <h2>Districts</h2>
        <div v-for="value in data['districts']" :key="value.id" class="district-card">  
          <district-card
            :modelValue="value"
          />
        </div>
      </div>
      <div class="card">
        <h2>Streets</h2>
        <div v-for="value in data['streets']" :key="value.id" class="street-card">  
          <street-card
            :modelValue="value"
          />
        </div>
      </div>
      
      
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import EditorCard from './components/EditorCard.vue'
import CitizenCard from './components/CitizenCard.vue'
import DistrictCard from './components/DistrictCard.vue'
import StreetCard from './components/StreetCard.vue'

const data = ref({})
const fileName = ref('')
function handleFile(event) {
  const file = event.target.files[0]
  fileName.value = file.name.replace('.cit', '')
  if (!file) return

  const reader = new FileReader()
  reader.onload = (e) => {
    try {
      const json = JSON.parse(e.target.result)
      data.value = {
        build: json.build,
        citizens: json.citizens,
        cityName: json.cityName,
        cityTiles: json.cityTiles,
        districts: json.districts,
        groups: json.groups,
        streets: json.streets,
      }
      console.log('Arquivo carregado:', data.value)
    } catch (err) {
      alert('Erro ao ler o arquivo JSON')
    }
  }
  reader.readAsText(file)
}

function downloadFile() {
  console.log('Baixando arquivo modificado:', data.value)
  const blob = new Blob([JSON.stringify(data.value, null, 2)], {
    type: 'application/json',
  })
  const link = document.createElement('a')
  link.href = URL.createObjectURL(blob)
  link.download = fileName.value + '_modified.cit'
  link.click()
}
</script>

<style>
body {
  margin: 0;
  font-family: 'Courier New', Courier, monospace;
  background-color: #111;
  color: #ddd;
}
h1 {
  color: #fff;
  text-align: center;
  margin: 0;
}
h2 {
  color: #fff;
  margin: 0.5rem;
}

.container {
  margin: auto;
}
.editor {
  background-color: #222;
  padding: 0 1rem;
  border-radius: 8px;
  margin-top: 1rem;
  display: flex;
}
input[type='file'] {
  margin-bottom: 1rem;
}
button {
  background-color: #333;
  color: #fff;
  padding: 0.7rem 1.2rem;
  border: 1px solid #666;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background-color: #555;
}
.list {
  display: grid;
  gap: 1rem;
  background-color: #222;
}
</style>
