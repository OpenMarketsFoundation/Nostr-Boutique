<script setup>
const props = defineProps({
  compact: {
    type: Boolean,
    default: false
  }
})

const logoSrc = ref('/Logo.png')

const handleLogoError = () => {
  if (logoSrc.value === '/Logo.png') {
    logoSrc.value = '/Nostr-Boutique-Logo.png'
    return
  }

  if (logoSrc.value === '/Nostr-Boutique-Logo.png') {
    logoSrc.value = '/nostr-boutique-logo.svg'
    return
  }

  logoSrc.value = ''
}
</script>

<template>
  <NuxtLink to="/" class="inline-flex items-center" aria-label="Nostr Boutique home">
    <img
      v-if="logoSrc"
      :src="logoSrc"
      alt="Nostr Boutique"
      :class="props.compact ? 'brand-logo brand-logo--invert h-11 w-auto' : 'brand-logo brand-logo--hero h-30 w-auto'"
      @error="handleLogoError"
    >
    <div v-else class="inline-flex flex-col leading-none">
      <span class="hero-title text-2xl font-black">Nostr Boutique</span>
    </div>
  </NuxtLink>
</template>
