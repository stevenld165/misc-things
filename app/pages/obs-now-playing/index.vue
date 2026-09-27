<script setup lang="ts">
import * as z from "zod"

const formSchema = z.object({
  username: z.string(),
  password: z.string(),
  serverUrl: z.string(),
})

const formState = reactive({
  username: "",
  password: "",
  serverUrl: "",
})

const generatedUrl = ref("")

const handleSubmit = () => {
  const param = btoa(JSON.stringify(formState))
  const requestURL = useRequestURL()

  generatedUrl.value = `${requestURL.href}/${param}`
}
</script>
<template>
  <div class="px-4 py-8">
    <h1 class="text-xl">Subsonic OBS Now Playing Widget Setup</h1>
    <p>
      This is the setup for my custom now playing widget. Currenly only supports
      Subsonic servers, but there are plans to add Spotify/YT Music support
    </p>

    <blockquote class="mt-4">
      NOTE: The generated URL will contain the sensitive information you type
      into this form. Please do not share the URL anywhere you do not trust. All
      info is stored on the URL which is very insecure, so I reccommend you only
      use this for a server that is not exposed to the internet.
    </blockquote>

    <UForm
      :schema="formSchema"
      :state="formState"
      @submit="handleSubmit"
      class="flex flex-col gap-4 items-baseline"
    >
      <UFormField label="Subsonic Server URL" name="serverUrl">
        <UInput v-model="formState.serverUrl" />
      </UFormField>

      <UFormField label="Username" name="username">
        <UInput v-model="formState.username" />
      </UFormField>

      <UFormField label="Password" name="password">
        <UInput v-model="formState.password" />
      </UFormField>

      <UButton type="submit"> Generate Widget URL </UButton>
    </UForm>

    <span v-if="generatedUrl">
      Generated URL: <NuxtLink :to="generatedUrl">{{ generatedUrl }}</NuxtLink>
    </span>
  </div>
</template>
<style lang="scss" scoped></style>
