<script setup>
const route = useRoute()
const { initTheme } = useThemeMode()
const isHome = computed(() => route.path === '/')
const isMenuOpen = ref(false)

const links = [
  { to: '/', label: 'Home' },
  { to: '/example', label: 'Example' },
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
    <header class="border-b" :style="{ borderColor: 'var(--line)', background: 'var(--bg)' }">
      <div class="mx-auto w-full max-w-6xl px-4 py-4 sm:px-6">
        <div class="flex items-center justify-between gap-3">
          <div class="flex min-w-0 items-center gap-3 sm:gap-5">
            <SiteBrand compact />
            <nav class="hidden min-w-0 items-center gap-2 overflow-x-auto md:flex md:gap-3" style="scrollbar-width: none;">
              <NuxtLink
                v-for="link in links"
                :key="link.to"
                :to="link.to"
                class="shrink-0 border px-3 py-1.5 text-center text-xs font-bold whitespace-nowrap transition sm:px-4 sm:py-2 sm:text-sm"
                :style="isActive(link.to) ? { borderColor: 'var(--text)', background: 'var(--text)', color: 'var(--bg)' } : { borderColor: 'var(--line)', color: 'var(--muted)' }"
              >
                {{ link.label }}
              </NuxtLink>
            </nav>
          </div>

          <div class="flex items-center gap-2">
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
            class="border px-3 py-2 text-center text-xs font-bold transition"
            :style="isActive(link.to) ? { borderColor: 'var(--text)', background: 'var(--text)', color: 'var(--bg)' } : { borderColor: 'var(--line)', color: 'var(--muted)' }"
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
