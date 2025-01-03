<template>
  <div class="flex space-x-2 items-center">
    <div class="text-gray-500 text-sm" v-if="showNextModeLabel">
      Change to {{ nextMode }}
    </div>
    <button
      @click="updateColorMode()"
      @mouseenter="showNextModeLabel = true"
      @mouseleave="showNextModeLabel = false"
      class="hover:bg-gray-100 dark:bg-gray-600 px-2 py-1 text-gray-500"
    >
      <MdiIcon :icon="modeIcons[nextMode]" size="1.5em" />
    </button>
  </div>
</template>
<script setup>
const showNextModeLabel = ref(false);
const colorMode = useColorMode();
const modes = ["system", "light", "dark"];
const modeIcons = {
  system: "mdiLightbulbOn50",
  light: "mdiLightbulbOnOutline",
  dark: "mdiLightbulbOn",
};
const nextMode = computed(() => {
  const currentModeIndex = modes.indexOf(colorMode.preference);
  const nextModeIndex = (currentModeIndex + 1) % modes.length;
  return modes[nextModeIndex];
});
function updateColorMode() {
  colorMode.preference = nextMode.value;
}
</script>
