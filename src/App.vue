<template>
  <v-app>
    <v-main>
      <div class="d-flex flex-column justify-center align-center">
        <h1 class="text-center">{{ $t('title') }}</h1>
        <v-row class="mt-4">
          <v-col>
            <v-file-input
              :label="$t('uploadFile')"
              hide-details
              :prepend-icon="null"
              counter
              variant="outlined"
              accept=".cit"
              width="500"
              clearable
              @change="handleFile"
              @click:clear="data = defaultData"
            />
          </v-col>
          <v-col class="d-flex align-center">
            <v-btn :disabled="!data" @click="downloadFile" :loading="loading" class="mr-3">
              {{ $t('downloadFile') }}
            </v-btn>
            <v-btn disabled color="pink" variant="outlined">
              {{ $t('resetData') }}
            </v-btn>
          </v-col>
        </v-row>

        <select v-model="locale" class="lang-select mt-3">
          <option value="en">🇺🇸 English</option>
          <option value="es">🇪🇸 Español</option>
          <option value="pt">🇧🇷 Português</option>
        </select>
      </div>

      <CategoryTabs :model-value="data" :loading="loading" />
    </v-main>
  </v-app>
</template>

<script setup>
import CategoryTabs from './components/CategoryTabs.vue'
import { useI18n } from 'vue-i18n'

const { locale } = useI18n()

const data = ref({})
const fileName = ref('')
const loading = ref(false)
const defaultData = ref({
  build: '',
  citySize: '',
  citizens: [],
  cityName: '',
  cityTiles: [],
  districts: [],
  groups: [],
  streets: [],
  population: '',
  seed: '',
})

function handleFile(event) {
  const file = event.target.files[0]
  fileName.value = file ? file.name.replace('.cit', '') : null
  if (!file) return
  loading.value = true

  const reader = new FileReader()
  reader.onload = (e) => {
    try {
      const json = JSON.parse(e.target.result)
      const loadedData = {
        build: json.build,
        citySize: json.citySize,
        citizens: json.citizens,
        cityName: json.cityName,
        cityTiles: json.cityTiles,
        districts: json.districts,
        groups: json.groups,
        streets: json.streets,
        population: json.population,
        seed: json.seed,
      }
      data.value = loadedData
    } catch (err) {
      alert('Erro ao ler o arquivo JSON')
    } finally {
      loading.value = false
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
html,
body,
#app {
  background-color: #0f0f0f;
  color: #0ff;
  font-family: 'Share Tech Mono', monospace;
}

.v-application {
  background-color: transparent !important;
}

h1 {
  font-size: 3rem;
  text-align: center;
  color: rgb(255, 0, 89);
  /* Neon ciano */
  text-shadow:
    0 0 5px rgb(255, 0, 89),
    0 0 10px rgb(255, 0, 89),
    0 0 20px rgb(255, 0, 89),
    0 0 40px rgb(255, 0, 89);
  animation: glowPulse 2s infinite alternate;
}

@keyframes glowPulse {
  from {
    text-shadow:
      0 0 5px rgb(255, 0, 89),
      0 0 10px rgb(255, 0, 89),
      0 0 20px rgb(255, 0, 89),
      0 0 40px rgb(255, 0, 89);
  }

  to {
    text-shadow:
      0 0 10px rgb(255, 0, 89),
      0 0 20px rgb(255, 0, 89),
      0 0 40px rgb(255, 0, 89),
      0 0 80px rgb(255, 0, 89);
  }
}

.lang-select {
  position: fixed;
  top: 5px;
  right: 15px;
  background-color: #1a1a1a;
  color: rgb(255, 0, 89);
  border: 1px solid rgb(255, 0, 89);
  padding: 6px 12px;
  border-radius: 5px;
  font-family: 'Share Tech Mono', monospace;
  font-size: 14px;
  z-index: 999;
}

.lang-select:focus {
  outline: none;
}
</style>
