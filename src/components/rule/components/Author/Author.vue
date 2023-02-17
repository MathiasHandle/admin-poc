<script setup>
import { computed, defineProps, inject } from 'vue'

import { ACTIONS } from '../../constants/actions'

const props = defineProps({
  mode: {
    type: String,
  },
})

const formData = inject('formData')

// Pouzity provide inject ak by to bolo moc zanorene
const inputText = computed({
  get: () => {
    return formData.author
  },
  set: (newValue) => {
    formData.author = newValue
  },
})
</script>

<template>
  <div class="wrapper">
    <label for="author">Author</label>
    <input name="author" type="text" v-model="inputText" :disabled="props.mode !== ACTIONS.edit" />
  </div>
</template>

<style lang="scss" scoped>
.wrapper {
  display: flex;
  flex-direction: column;
}
</style>
