<script setup lang="ts">
import type { Song } from "~/types/song"

const props = defineProps<{
  song: Song
}>()
</script>
<template>
  <div
    class="bg-red-400 rounded-full m-auto max-w-sm text-white transition-all ease-in-out"
    :style="{
      background: `url(${song.coverArt})`,
      backgroundSize: 'cover',
    }"
  >
    <div
      class="flex p-1 gap-4 items-center rounded-full backdrop-blur-xl shadow-md"
      style="background: rgba(0, 0, 0, 0.1)"
    >
      <div
        class="min-w-24 min-h-24 w-24 h-24 rounded-full transition-all ease-in-out shadow-lg"
        :style="{
          background: `url(${song.coverArt})`,
          backgroundSize: 'cover',
        }"
      ></div>

      <div class="flex flex-col gap-2 truncate">
        <div>
          <h2 class="font-bold text-lg flex items-center gap-2 w-[90%]">
            <Icon class="shrink-0" name="reicon:music-note-filled" />
            <UMarquee :overlay="false">
              <span>{{ song.title }}</span>
            </UMarquee>
          </h2>
          <span class="">{{ song.artist }}</span>
        </div>

        <span class="text-sm italic font-light">{{ song.album }}</span>
      </div>
    </div>
  </div>
</template>
<style lang="scss" scoped></style>
