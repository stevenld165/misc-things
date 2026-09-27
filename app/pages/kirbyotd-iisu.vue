<script setup lang="ts">
import { KIRBYOTD_API } from "~/constants/constants"

type KirbyOTDResponse = {
  ability: string
  img: string
}

const { data: kirbyOtd } = await useFetch<KirbyOTDResponse>(KIRBYOTD_API)
</script>
<template>
  <div
    class="kirbyotd-container p-4 flex flex-col items-center justify-center h-screen gap-2"
  >
    <img :src="kirbyOtd?.img" />
    <div class="bg-white py-1 px-2 rounded-full shadow-lg">
      <span class="text-pink-gradient text-sm">
        {{ kirbyOtd?.ability.toLocaleLowerCase() }} kirby!
      </span>
    </div>
  </div>
</template>
<style lang="scss" scoped>
.kirbyotd-container {
  background: radial-gradient(88.91% 165.67% at 76.5% 29.12%, #ff989b, #b07cf0);
}

.text-pink-gradient {
  background: radial-gradient(
      88.91% 165.67% at 76.5% 29.12%,
      #ff989b 0%,
      #b07cf0 100%
    )
    /* warning: gradient uses a rotation that is not supported by CSS and may not behave as expected */;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-fill-color: transparent;
}

img {
  filter: drop-shadow(2px 0 0 #ffffff) drop-shadow(-2px 0 0 #ffffff)
    drop-shadow(0 2px 0 #ffffff) drop-shadow(0 -2px 0 #ffffff)
    drop-shadow(2px 2px 5px #24242467);
}
</style>
