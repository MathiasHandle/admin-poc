<script setup>
import { computed, defineProps, defineEmits } from 'vue'

import { ACTIONS } from '../../../constants/actions'

const props = defineProps({
  mode: {
    type: String,
  },
  modelValue: {
    type: String,
  },
})

// Univerzalny input riadeny z TimeWrapper.vue
// Mozes spravit univerzalnu komponentu ktora zvladne "time", "date" a "datetime-local", ked posles propku s "type" pre input
const emit = defineEmits(['update:modelValue'])
const inputText = computed({
  get: () => {
    return props.modelValue
  },
  set: (newValue) => {
    emit('update:modelValue', newValue)
  },
})
</script>

<template>
  <div class="wrapper">
    <label for="author">Time</label>
    <input name="author" type="date" v-model="inputText" :disabled="props.mode !== ACTIONS.edit" />
  </div>
</template>

<style lang="scss">
.wrapper {
  display: flex;
  flex-direction: column;
}
</style>
