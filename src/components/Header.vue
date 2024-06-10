<template>
  <VAppBar>
    <VAppBarTitle>🎯 Todo-SPA | Viviarto</VAppBarTitle>
    <VSpacer />
    <VSwitch
      hide-details
      class="mr-4"
      v-model="darkTheme"
      :label="darkTheme ? 'Light Theme' : 'Dark Theme'"
      @change="toggleTheme"
    />
  </VAppBar>
</template>

<script setup>
import { useTheme } from "vuetify";
import { VAppBar, VAppBarTitle, VSpacer, VSwitch } from "vuetify/components";

const theme = useTheme();

function toggleTheme() {
  theme.global.name.value = theme.global.current.value.dark ? "light" : "dark";
}
</script>

<style scoped></style>
