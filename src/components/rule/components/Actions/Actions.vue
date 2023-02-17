<script setup>
import { defineEmits } from 'vue'

import { ACTIONS } from '../../constants/actions'

// Zmena modu v ktorom je formular
// Ak to mas moc zanorene tak mozes opat pouzit provide inject, akorat by som dal samostatny state na to
const emit = defineEmits(['modeUpdate'])
const handleClick = (action) => {
  emit('modeUpdate', action)
}
</script>

<template>
  <div class="wrapper">
    <button type="submit" @click="() => handleClick(ACTIONS.save)">SAVE</button>
    <button type="button" @click="() => handleClick(ACTIONS.edit)">EDIT</button>
  </div>
</template>

<style lang="scss" scoped>
.wrapper {
  display: flex;
  gap: 30px;
}

button {
  border-radius: 5px;
  border: none;
  outline: none;

  &:hover {
    cursor: pointer;
  }
}
</style>
