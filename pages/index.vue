<script setup>
useSeoMeta({
  title: 'Nostr Boutique',
  description: 'Host your own self sovereign shop.'
})
</script>

<template>
  <section class="w-full max-w-3xl text-center">
    <div class="flex justify-center">
      <SiteBrand />
    </div>

    <NsiteClonePanel />
  </section>
</template>
