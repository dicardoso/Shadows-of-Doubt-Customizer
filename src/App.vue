<template>
  <v-app>
    <v-main>
      <div class="d-flex flex-column justify-center align-center">

        <h1 class="text-center">City Editor</h1>

        <v-btn class="mt-3">{{ $t('downloadFile') }}</v-btn>

        <select v-model="locale" class="lang-select mt-3">
          <option value="pt">🇧🇷 Português</option>
          <option value="en">🇺🇸 English</option>
        </select>
      </div>

      <CategoryTabs />
    </v-main>
  </v-app>
</template>

<script setup>
import CategoryTabs from './components/CategoryTabs.vue'
import { useI18n } from 'vue-i18n'

const { locale } = useI18n()
</script>

<style>
html,
body,
#app {
  background-color: #0f0f0f;
  color: #0ff;
  font-family: 'Share Tech Mono', monospace;
  /* Dá um ar cyberpunk */
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
    0 0 40px rgb(255, 0, 89),
    0 0 80px rgb(255, 0, 89);
  animation: glowPulse 2s infinite alternate;
}

@keyframes glowPulse {
  from {
    text-shadow:
      0 0 5px rgb(255, 0, 89),
      0 0 10px rgb(255, 0, 89),
      0 0 20px rgb(255, 0, 89),
      0 0 40px rgb(255, 0, 89),
      0 0 80px rgb(255, 0, 89);
  }

  to {
    text-shadow:
      0 0 10px rgb(255, 0, 89),
      0 0 20px rgb(255, 0, 89),
      0 0 40px rgb(255, 0, 89),
      0 0 80px rgb(255, 0, 89),
      0 0 160px rgb(255, 0, 89);
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
