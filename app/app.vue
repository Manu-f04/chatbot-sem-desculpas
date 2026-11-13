
<script setup>
useHead({
  meta: [
    {
      name: 'viewport',
      content: 'width=device-width, initial-scale=1'
    }
  ],
  link: [
    { rel: 'icon', href: '/favicon.ico' }
  ],
  htmlAttrs: {
    lang: 'pt-BR'
  }
})

const title = 'SEM DESCULPAS'
const description = 'Seu choque de realidade diário.'

useSeoMeta({
  title,
  description,
  ogTitle: title,
  ogDescription: description
})
</script>

<template>
  <UApp>
    <NuxtPage />
  </UApp>
</template>

<style>
* {
  box-sizing: border-box;
}

html,
body,
#__nuxt {
  margin: 0;
  padding: 0;
  min-height: 100%;
  background-color: #121212;
  color: #ffffff;
}
</style>
