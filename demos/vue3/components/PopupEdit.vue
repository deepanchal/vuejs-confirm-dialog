<script setup lang="ts">
import { onMounted, ref, PropType} from 'vue'
import { useFocus } from '@vueuse/core'

const { value, event } = defineProps({
  value: {
    type: String,
  },
  event: {
    type: Object as PropType<PointerEvent>
  }
})

const model = ref('')

onMounted(() => {
  model.value = value
})

const emit = defineEmits(['confirm', 'cancel'])
</script>

<template>
  <div class="my-modal" @click.self="emit('cancel')">
    <div class="popup-box" :style="{ 'top': event.pageY + 'px', 'left': event.pageX + 'px' }">
      <div class="popup-action">
        <input
          type="text"
          v-model="model"
          placeholder="Type here"
          class="input input-bordered w-full"
        />
        <button class="btn btn-primary" @click="emit('confirm', model)">
          Save
        </button>
      </div>
    </div>
  </div>
</template>

<style>
.popup-box {
  position: absolute;
    --tw-bg-opacity: 1;
    background-color: hsla(var(--b1) / var(--tw-bg-opacity, 1));
    padding: 15px 10px;
    width: 300px;
    transform: translateX(var(--tw-translate-x)) translateY(var(--tw-translate-y)) rotate(var(--tw-rotate)) skewX(var(--tw-skew-x)) skewY(var(--tw-skew-y)) scaleX(var(--tw-scale-x)) scaleY(var(--tw-scale-y));
    transition-property: background-color, border-color, color, fill, stroke, opacity, box-shadow, transform;
    transition-duration: .15s;
    transition-duration: .2s;
    transition-timing-function: cubic-bezier(.4, 0, .2, 1);
    border-radius: var(--rounded-box, 1rem);
    box-shadow: 0 25px 50px -12px rgb(0 0 0 / 25%);
}

.popup-action {
    display: flex;
    justify-content: flex-end;
}
</style>
