<script setup>
const exampleCloudUrl = 'https://npub1equrmqway3qxw3dkssymusxkwgwrqypfgeqx0lx9pgjam7gnj4ysaqhkj6.nsite.cloud/'
const exampleRunUrl = 'https://npub1equrmqway3qxw3dkssymusxkwgwrqypfgeqx0lx9pgjam7gnj4ysaqhkj6.nsite.run/'
const exampleLolUrl = 'https://npub1equrmqway3qxw3dkssymusxkwgwrqypfgeqx0lx9pgjam7gnj4ysaqhkj6.nsite.lol/'
const previewTarget = ref('lol')

const previewUrl = computed(() => {
  if (previewTarget.value === 'cloud') return exampleCloudUrl
  if (previewTarget.value === 'run') return exampleRunUrl
  return exampleLolUrl
})

useSeoMeta({
  title: 'Example | Nostr Boutique',
  description: 'View a live Nsite deployment that demonstrates the Nostr Boutique template direction.'
})
</script>

<template>
  <section class="fade-in-up grid gap-4 lg:grid-cols-[1fr_1.1fr]">
    <article class="surface-card p-6 sm:p-8">
      <span class="pill">Reference deployment</span>
      <h1 class="hero-title mt-4 text-4xl font-black leading-tight">See a live Gamma-style Nsite.</h1>
      <p class="mt-4 text-sm sm:text-base" :style="{ color: 'var(--muted)' }">
        This example is the public storefront used as a proof point for this landing site.
        You can open it directly and inspect how a Nostr-hosted merchant surface behaves.
      </p>

      <div class="mt-6 grid gap-3">
        <a
          :href="exampleRunUrl"
          target="_blank"
          rel="noopener noreferrer"
          class="cta-primary inline-flex items-center justify-center rounded-full px-5 py-2.5 text-sm font-black"
        >
          Open live example
        </a>
        <a
          :href="exampleCloudUrl"
          target="_blank"
          rel="noopener noreferrer"
          class="inline-flex items-center justify-center rounded-full border px-5 py-2.5 text-sm font-bold"
          :style="{ borderColor: 'var(--line)' }"
        >
          Open via nsite.cloud
        </a>
        <a
          :href="exampleLolUrl"
          target="_blank"
          rel="noopener noreferrer"
          class="inline-flex items-center justify-center rounded-full border px-5 py-2.5 text-sm font-bold"
          :style="{ borderColor: 'var(--line)' }"
        >
          Open via nsite.lol
        </a>
        <NuxtLink to="/explore" class="inline-flex items-center justify-center rounded-full border px-5 py-2.5 text-sm font-bold" :style="{ borderColor: 'var(--line)' }">
          Explore related Nsites
        </NuxtLink>
      </div>

    </article>

    <article class="surface-card overflow-hidden p-3">
      <div class="mb-3 flex items-center gap-2 border px-3 py-2" :style="{ borderColor: 'var(--line)' }">
        <span class="h-2.5 w-2.5 rounded-full" :style="{ background: 'var(--muted)' }" />
        <span class="h-2.5 w-2.5 rounded-full" :style="{ background: 'var(--muted)' }" />
        <span class="h-2.5 w-2.5 rounded-full" :style="{ background: 'var(--muted)' }" />
        <span class="ml-2 truncate text-xs" :style="{ color: 'var(--muted)' }">{{ previewUrl }}</span>
      </div>

      <iframe
        title="Nostr Boutique Example Nsite"
        :src="previewUrl"
        class="h-[68vh] w-full rounded-xl border"
        :style="{ borderColor: 'var(--line)' }"
        loading="lazy"
      />
    </article>
  </section>

  <section class="mt-6 grid gap-4 md:grid-cols-3">
    <article class="panel">
      <h2 class="text-base font-black">Real deployment</h2>
      <p class="mt-2 text-sm" :style="{ color: 'var(--muted)' }">Not a mockup. This is a live nsite URL visitors can test.</p>
    </article>
    <article class="panel">
      <h2 class="text-base font-black">Works on gateways</h2>
      <p class="mt-2 text-sm" :style="{ color: 'var(--muted)' }">Accessed through gateway infrastructure so regular browsers can render it via nsite.cloud, nsite.run, and nsite.lol.</p>
    </article>
    <article class="panel">
      <h2 class="text-base font-black">Template reference</h2>
      <p class="mt-2 text-sm" :style="{ color: 'var(--muted)' }">Use this as the baseline behavior while shaping your own storefront.</p>
    </article>
  </section>
</template>
