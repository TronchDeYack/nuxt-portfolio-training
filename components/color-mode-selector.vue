<script setup>
const colorMode = useColorMode()

const modes = ['system', 'light', 'dark']

const nextMode = computed(() => {
  const currentModeIndex = modes.indexOf(colorMode.preference)
  if (currentModeIndex + 1 === modes.length) return modes[0]
  return modes[currentModeIndex + 1]
})

const nextModeIcon = computed(() => nextModeIcons[nextMode.value])

const nextModeIcons = {
  system: '🌓',
  light: '🌕',
  dark: '🌑',
}

function toggle () {
  colorMode.preference = nextMode.value
}

const showNextModeLabel = ref(false)
</script>

<template>
  <div class="flex space-x-2 items-center">
    <div class="text-gray-500 text-xs" v-if="showNextModeLabel">Change to {{ nextMode }}</div>
    <button 
      @click="toggle()" 
      @mouseenter="showNextModeLabel = true"
      @mouseleave="showNextModeLabel = false"
      class="hover:bg-gray-200 dark:hover:bg-gray-600 px-2 py-1 text-gray-500 text-4xl md:text-base"
    >
      {{ nextModeIcon }}
    </button>
  </div>
</template>
