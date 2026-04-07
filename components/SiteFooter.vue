<script setup>
const route = useRoute()

const isActive = (path) => route.path === path
</script>

<template>
  <footer class="border-t" :style="{ borderColor: 'var(--line)', background: 'var(--chrome-bg)' }">
    <div class="mx-auto w-full max-w-6xl px-4 py-6 sm:px-6">
      <div class="grid gap-4 sm:grid-cols-[1.2fr_1fr] sm:items-end">
        <div class="flex justify-center sm:justify-start">
          <SiteBrand compact />
        </div>
        <div class="flex flex-wrap items-center justify-center gap-2 text-sm sm:justify-end">
          <NuxtLink to="/" class="px-2 py-1 text-sm font-semibold" :style="isActive('/') ? { color: 'var(--text)', boxShadow: 'inset 0 -2px 0 var(--menu-active-underline)' } : { color: 'var(--muted)' }">Home</NuxtLink>
          <NuxtLink to="/example" class="px-2 py-1 text-sm font-semibold" :style="isActive('/example') ? { color: 'var(--text)', boxShadow: 'inset 0 -2px 0 var(--menu-active-underline)' } : { color: 'var(--muted)' }">Example</NuxtLink>
          <NuxtLink to="/themes" class="px-2 py-1 text-sm font-semibold" :style="isActive('/themes') ? { color: 'var(--text)', boxShadow: 'inset 0 -2px 0 var(--menu-active-underline)' } : { color: 'var(--muted)' }">Themes</NuxtLink>
          <NuxtLink to="/explore" class="px-2 py-1 text-sm font-semibold" :style="isActive('/explore') ? { color: 'var(--text)', boxShadow: 'inset 0 -2px 0 var(--menu-active-underline)' } : { color: 'var(--muted)' }">Explore</NuxtLink>
          <NuxtLink to="/explain" class="px-2 py-1 text-sm font-semibold" :style="isActive('/explain') ? { color: 'var(--text)', boxShadow: 'inset 0 -2px 0 var(--menu-active-underline)' } : { color: 'var(--muted)' }">Explain</NuxtLink>
          <a
            href="https://github.com/openmarketsfoundation"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex h-8 w-8 items-center justify-center rounded-full border"
            :style="{ borderColor: 'var(--line)', color: 'var(--text)', background: 'var(--bg-soft)' }"
            aria-label="Open Open Markets Foundation GitHub"
            title="Open Markets Foundation GitHub"
          >
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="h-4 w-4" aria-hidden="true">
              <path d="M12 .5C5.65.5.5 5.66.5 12.02c0 5.1 3.3 9.42 7.88 10.95.58.1.79-.25.79-.56 0-.27-.01-1-.02-1.97-3.2.7-3.88-1.54-3.88-1.54-.52-1.33-1.28-1.68-1.28-1.68-1.04-.72.08-.71.08-.71 1.15.08 1.75 1.18 1.75 1.18 1.02 1.75 2.68 1.25 3.33.96.1-.74.4-1.25.72-1.54-2.55-.29-5.24-1.28-5.24-5.69 0-1.26.45-2.29 1.18-3.09-.12-.29-.51-1.46.11-3.05 0 0 .96-.31 3.14 1.18a10.9 10.9 0 0 1 5.72 0c2.18-1.49 3.14-1.18 3.14-1.18.62 1.59.23 2.76.11 3.05.74.8 1.18 1.83 1.18 3.09 0 4.42-2.69 5.39-5.25 5.68.41.35.78 1.05.78 2.11 0 1.52-.01 2.75-.01 3.12 0 .31.21.67.8.56a11.53 11.53 0 0 0 7.87-10.95C23.5 5.66 18.35.5 12 .5Z"/>
            </svg>
          </a>
        </div>
      </div>

      <p class="mt-4 text-center text-xs" :style="{ color: 'var(--muted)' }">
        © Nostr.boutique 2026
      </p>
      </div>
  </footer>
</template>
