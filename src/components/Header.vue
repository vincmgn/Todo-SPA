<template>
  <VAppBar class="px-5">
    <!-- Title -->
    <VAppBarTitle>🎯 Todo-SPA</VAppBarTitle>
    <!-- Spacer -->
    <VSpacer />
    <!-- Dark theme Switch -->
    <VSwitch
      hide-details
      class="mr-4"
      v-model="darkTheme"
      :label="darkTheme ? 'Dark Theme' : 'Light Theme'"
      @change="toggleTheme"
    />
  </VAppBar>
</template>

<script setup>
// IMPORTS
import { ref } from "vue";
import { useTheme } from "vuetify";
import { VAppBar, VAppBarTitle, VSpacer, VSwitch } from "vuetify/components";

// DATA
const theme = useTheme();
const darkTheme = ref(theme.global.current.value.dark); // setup dark theme

// METHODS
function toggleTheme() {
  // if dark theme is enabled, switch to light theme
  theme.global.name.value = theme.global.current.value.dark ? "light" : "dark";
}
</script>

<style scoped>
@media screen and (max-width: 650px) {
  .v-spacer {
    display: none;
  }
}
</style>
