<script setup>
import { computed, defineProps, inject } from 'vue'

import Time from './components/TimeInput.vue'

const props = defineProps({
  mode: {
    type: String,
  },
})

const formData = inject('formData')

//Nadriadena komponenta pre casove sloty, spravujes tu naraz time.start a time.end
// data z inputov tu idu cez emity (su len o 1 uroven nizsie a su to univerzalne komponenty)
// ale do formulara to posielas cez provide/inject (ak by to bolo moc zanorene)
const inputStart = computed({
  get: () => {
    return formData.time.start
  },
  set: (newValue) => {
    formData.time.start = newValue
  },
})

const inputEnd = computed({
  get: () => {
    return formData.time.end
  },
  set: (newValue) => {
    formData.time.end = newValue
  },
})
</script>

<template>
  <Time :mode="props.mode" v-model="inputStart" />
  <Time :mode="props.mode" v-model="inputEnd" />
</template>
