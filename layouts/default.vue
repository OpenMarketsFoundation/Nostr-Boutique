<script setup>
const route = useRoute()
const { initTheme } = useThemeMode()
const isHome = computed(() => route.path === '/')
const isMenuOpen = ref(false)

const links = [
  { to: '/', label: 'Home' },
  { to: '/example', label: 'Example' },
  { to: '/themes', label: 'Themes' },
  { to: '/explore', label: 'Explore' },
  { to: '/explain', label: 'Explain' }
]

onMounted(() => {
  initTheme()
})

watch(() => route.path, () => {
  isMenuOpen.value = false
})

const isActive = (path) => route.path === path
</script>

<template>
  <div class="site-shell flex min-h-screen flex-col">
    <header class="border-b" :style="{ borderColor: 'var(--line)', background: 'var(--chrome-bg)' }">
      <div class="mx-auto w-full max-w-6xl px-4 py-4 sm:px-6">
        <div class="flex items-center justify-between gap-3">
          <SiteBrand compact />

          <nav class="hidden min-w-0 flex-1 items-center justify-center gap-2 overflow-x-auto md:flex md:gap-3" style="scrollbar-width: none;">
            <NuxtLink
              v-for="link in links"
              :key="link.to"
              :to="link.to"
              class="shrink-0 px-3 py-1.5 text-center text-xs font-bold whitespace-nowrap transition sm:px-4 sm:py-2 sm:text-sm"
              :style="isActive(link.to) ? { color: 'var(--text)', boxShadow: 'inset 0 -3px 0 var(--menu-active-underline)' } : { color: 'var(--muted)' }"
            >
              {{ link.label }}
            </NuxtLink>
          </nav>

          <div class="flex items-center gap-2">
            <a
              href="https://github.com/openmarketsfoundation"
              target="_blank"
              rel="noopener noreferrer"
              class="inline-flex h-9 w-9 items-center justify-center rounded-full border transition"
              :style="{ borderColor: 'var(--line)', color: 'var(--text)', background: 'var(--bg-soft)' }"
              aria-label="Open Open Markets Foundation GitHub"
              title="Open Markets Foundation GitHub"
            >
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="h-4 w-4" aria-hidden="true">
                <path d="M12 .5C5.65.5.5 5.66.5 12.02c0 5.1 3.3 9.42 7.88 10.95.58.1.79-.25.79-.56 0-.27-.01-1-.02-1.97-3.2.7-3.88-1.54-3.88-1.54-.52-1.33-1.28-1.68-1.28-1.68-1.04-.72.08-.71.08-.71 1.15.08 1.75 1.18 1.75 1.18 1.02 1.75 2.68 1.25 3.33.96.1-.74.4-1.25.72-1.54-2.55-.29-5.24-1.28-5.24-5.69 0-1.26.45-2.29 1.18-3.09-.12-.29-.51-1.46.11-3.05 0 0 .96-.31 3.14 1.18a10.9 10.9 0 0 1 5.72 0c2.18-1.49 3.14-1.18 3.14-1.18.62 1.59.23 2.76.11 3.05.74.8 1.18 1.83 1.18 3.09 0 4.42-2.69 5.39-5.25 5.68.41.35.78 1.05.78 2.11 0 1.52-.01 2.75-.01 3.12 0 .31.21.67.8.56a11.53 11.53 0 0 0 7.87-10.95C23.5 5.66 18.35.5 12 .5Z"/>
              </svg>
            </a>
            <SiteThemeToggle />
            <button
              type="button"
              class="inline-flex h-9 w-9 items-center justify-center border md:hidden"
              :style="{ borderColor: 'var(--line)' }"
              :aria-expanded="isMenuOpen ? 'true' : 'false'"
              aria-label="Toggle navigation menu"
              @click="isMenuOpen = !isMenuOpen"
            >
              <svg
                v-if="!isMenuOpen"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                class="h-4 w-4"
                aria-hidden="true"
              >
                <path d="M4 6h16" />
                <path d="M4 12h16" />
                <path d="M4 18h16" />
              </svg>
              <svg
                v-else
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                class="h-4 w-4"
                aria-hidden="true"
              >
                <path d="M18 6 6 18" />
                <path d="m6 6 12 12" />
              </svg>
            </button>
          </div>
        </div>

        <nav v-if="isMenuOpen" class="mt-3 grid grid-cols-2 gap-2 md:hidden">
          <NuxtLink
            v-for="link in links"
            :key="`mobile-${link.to}`"
            :to="link.to"
            class="px-3 py-2 text-center text-xs font-bold transition"
            :style="isActive(link.to) ? { color: 'var(--text)', boxShadow: 'inset 0 -3px 0 var(--menu-active-underline)' } : { color: 'var(--muted)' }"
          >
            {{ link.label }}
          </NuxtLink>
        </nav>
      </div>
    </header>

    <main :class="isHome ? 'w-full flex-1' : 'mx-auto w-full max-w-6xl flex-1 px-4 py-8 sm:px-6'">
      <slot />
    </main>

    <SiteFooter />
  </div>
</template>
