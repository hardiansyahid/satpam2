<script setup lang="ts">
import type { NuxtError } from '#app'

const props = defineProps({
  error: Object as () => NuxtError
})
</script>

<template>
  <div>
    <h1>{{ error.statusCode }} Terjadi Kesalahan</h1>
    <NuxtLink to="/">Kembali Ke Beranda</NuxtLink>
  </div>
</template>
