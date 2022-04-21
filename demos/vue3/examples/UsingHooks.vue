<script lang="ts" setup>
import ModalWindow from './../components/SimpleModal.vue'
import { createConfirmDialog } from '../../../src/createConfirmDialog' 
import { ref } from 'vue'
import { debouncedWatch } from '@vueuse/core'

const defaultMessage = 'To prompt Modal Dialog press one of the buttons below:'
const message = ref(defaultMessage)

// Example how to use `createConfirmDialog` with hooks
// pass your modal component to the function
const { reveal, onConfirm, onCancel } = createConfirmDialog(ModalWindow)
onConfirm(() => {
  message.value = 'Confirmed!'
})
onCancel(() => {
  message.value = 'Canceled!'
})

debouncedWatch(
  message,
  () => {
    message.value = defaultMessage
  },
  { debounce: 2000 }
)

</script>

<template>
    <div class="card shadow-xl">
    <div class="justify-end card-body">
      <h1 class="card-title">Example of using hooks</h1>
      <p class="text-error">{{ message }}</p>
      <div class="card-actions">
        <button class="btn btn-primary" @click="reveal">Dialog</button>
      </div>
    </div>
  </div>
</template>