<script setup lang="ts">
import { SubsonicAPI } from "subsonic-api"
import type { Song } from "~/types/song"
import type { SubsonicInfo } from "~/types/subsonic-info"

const props = defineProps<{
  info: SubsonicInfo
}>()

const currentSong = ref<Song>({
  title: "No song currently playing...",
  album: "",
  artist: "",
  coverArt: "",
})

const fetchNowPlaying = async () => {
  const api = new SubsonicAPI({
    url: props.info.serverUrl,
    auth: {
      username: props.info.username,
      password: props.info.password,
    },
  })

  const { nowPlaying } = await api.getNowPlaying()

  if (nowPlaying.entry && nowPlaying.entry.length > 0) {
    const entry = nowPlaying.entry[0]!

    const coverArt = await api.getCoverArtURL({
      id: entry.coverArt ?? "",
    })

    if (currentSong.value.title != entry.title)
      currentSong.value = {
        title: entry.title,
        artist: entry.artist ?? "",
        album: entry.album ?? "",
        coverArt: coverArt,
      }
  } else {
    currentSong.value = {
      title: "",
      album: "",
      artist: "",
      coverArt: "",
    }
  }
}

let intervalId: number | null | undefined = null

onMounted(() => {
  fetchNowPlaying()

  intervalId = setInterval(() => {
    fetchNowPlaying()
  }, 10000)
})

onUnmounted(() => {
  if (intervalId) {
    clearInterval(intervalId)
  }
})
</script>
<template>
  <div v-if="currentSong.title">
    <ObsNowPlayingWidgetSongDisplayCard :song="currentSong" />
  </div>
</template>
<style lang="scss" scoped></style>
