<script setup lang="ts">
const route = useRoute()

const userInfo = computed(
  () =>
    typeof route.params.info == "string" && JSON.parse(atob(route.params.info)),
)
</script>
<template>
  <ObsNowPlayingWidgetNowPlaying v-if="userInfo" :info="userInfo" />
</template>
<style lang="scss" scoped></style>
