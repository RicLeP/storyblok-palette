<script setup lang="ts">
import { useFieldPlugin } from '@storyblok/field-plugin/vue3'
import Swatch from './Swatch.vue'
import { ref, watch } from 'vue'

const plugin = useFieldPlugin()

const defaultColours = [
  { value: '#fff', name: 'white' },
  { value: '#000', name: 'black' },
  // { value: 'linear-gradient(90deg,rgba(131, 58, 180, 1) 0%, rgba(253, 29, 29, 1) 50%, rgba(252, 176, 69, 1) 100%)', name: 'gradient' }
]

const parseSwatches = (swatches: string) => {
  try {
    return JSON.parse(swatches)
  } catch (e) {
    console.error('Failed to parse swatches:', e)
    return defaultColours
  }
}

const colours = ref(defaultColours)

watch(() => plugin.data?.options.swatches, (newSwatches) => {
  if (newSwatches) {
    colours.value = parseSwatches(newSwatches)
  }
})

const selectedColour = ref(colours.value[0])

const handleSave = (colour: { value: string; name: string; }) => {
  selectedColour.value = colour
  plugin.actions?.setContent(colour)
}
</script>

<template>
  <div class="palette">
    <swatch
      v-for="colour in colours"
      :key="colour.value"
      :colour="colour"
      :selected="selectedColour"
      @click="handleSave(colour)"
    />
  </div>
</template>

<style scoped lang="postcss">
.palette {
  display: grid;

  gap: 12px;

  grid-template-columns: repeat(auto-fit, 38px);
}
</style>