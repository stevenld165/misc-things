<script setup lang="ts">
import type { NavigationMenuItem } from "@nuxt/ui"

const items = ref<NavigationMenuItem[]>([
  { label: "Custom Now Playing OBS Widget" },
  { label: "KirbyOTD iiSU Style Widget", to: "/kirbyotd-iisu" },
])
</script>
<template>
  <div>
    <h1>My Miscellaneous Things</h1>
    <UNavigationMenu :items="items" orientation="vertical" />
  </div>
</template>
<style lang="scss" scoped></style>
