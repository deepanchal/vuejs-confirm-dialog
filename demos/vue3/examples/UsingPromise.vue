<script lang="ts" setup>
import ModalWindow from './../components/SimpleModal.vue'
import { createConfirmDialog } from '../../../src/createConfirmDialog' 
import { ref } from 'vue'
import { debouncedWatch } from '@vueuse/core'

// Pass new props of modal component in a second argument if you need to
const dialog = createConfirmDialog(ModalWindow, {
  msg: 'Modal #2',
})

// Build an async function to use it in a template
const showDialog = async () => {
  const { data, isCanceled } = await dialog.reveal({ msg: 'New Message!' }) // pass new props to modal component
  if (!isCanceled) message.value = 'Confirmed dialog #2!'
  else message.value = 'Canceled dialog #2!'
}

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
        <button class="btn btn-primary" @click="showDialog">Dialog</button>
      </div>
    </div>
  </div>
</template>