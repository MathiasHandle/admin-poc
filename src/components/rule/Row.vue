<script setup>
import { ref, provide } from 'vue'

import Author from './components/Author/Author.vue'
import TimeWrapper from './components/Time/TimeWrapper.vue'
import Actions from './components/Actions/Actions.vue'
import { ACTIONS } from './constants/actions.js'

// Data pre formular, ktore posielas na API
const formData = ref({
  author: '',
  time: {
    start: '',
    end: '',
  },
})
//Tu ich providujes dole do komponent
provide('formData', formData.value)

// Mod v ktorom sa nachadza form
// Zapina/vypina "disabled" na inputoch, ak to staci takto, tak nemusis robit extra dialog pre editaciu
// Akorat by som sa este zamyslel ako dostat tento state do TimeInput komponenty, bez prop drillingu
// mozno opat provide/inject ? .... mozno to neni problem?
const currentMode = ref(ACTIONS.display)

// Zavola sa na submit formulara -> click na SAVE tlacitko
const handleSubmit = () => {
  console.log('HANDLE SUBMIT')
  // tu posles data na API

  // a vyresetujes state na display nech sa dostanes z EDIT modu
  currentMode.value = ACTIONS.display
}
</script>

<template>
  <div class="wrapper">
    <form @submit.prevent="handleSubmit">
      <fieldset>
        <Author :mode="currentMode" />
      </fieldset>

      <fieldset>
        <TimeWrapper :mode="currentMode" />
      </fieldset>

      <fieldset>
        <Actions @mode-update="(newMode) => (currentMode = newMode)" />
      </fieldset>
    </form>

    <p>Mod: {{ currentMode }}</p>

    <div>
      <h4>Vypis dat</h4>
      <p>author: {{ formData.author }}</p>
      <p>start: {{ formData.time.start }}</p>
      <p>start: {{ formData.time.end }}</p>
    </div>
  </div>
</template>

<style lang="scss">
.wrapper {
  margin: 0 auto;
  width: fit-content;
}

form {
  display: flex;
  gap: 10px;

  fieldset: {
    border: none;
    outline: none;
  }
}
</style>
