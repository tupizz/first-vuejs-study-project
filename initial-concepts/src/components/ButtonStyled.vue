<template>
  <button class="button-styled">{{ text }}</button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  setup() {
    return {}
  },
  props: {
    text: {
      type: String,
      default: 'Botão'
    }
  }
})
</script>

<style scoped>
.button-styled {
  color: #fff;
  border-radius: 0.3rem;
  padding: 0.5rem 1rem;
  outline: none;
  border: none;
  cursor: pointer;
  display: block;
  margin-bottom: 1rem;
  background-color: #2d6cea;
}
</style>
