<script setup>
const { theme, toggleTheme } = useThemeMode()
</script>

<template>
  <button
    type="button"
    class="inline-flex h-9 w-9 items-center justify-center rounded-full border"
    :style="{ borderColor: 'var(--line)', background: 'var(--bg-soft)' }"
    @click="toggleTheme"
    :aria-label="theme === 'dark' ? 'Switch to light mode' : 'Switch to dark mode'"
  >
    <svg
      v-if="theme === 'dark'"
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      stroke-width="2"
      class="h-4 w-4"
      :style="{ color: 'var(--text)' }"
      aria-hidden="true"
    >
      <circle cx="12" cy="12" r="4" />
      <path d="M12 2v2" />
      <path d="M12 20v2" />
      <path d="m4.93 4.93 1.41 1.41" />
      <path d="m17.66 17.66 1.41 1.41" />
      <path d="M2 12h2" />
      <path d="M20 12h2" />
      <path d="m6.34 17.66-1.41 1.41" />
      <path d="m19.07 4.93-1.41 1.41" />
    </svg>
    <svg
      v-else
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      stroke-width="2"
      class="h-4 w-4"
      :style="{ color: 'var(--text)' }"
      aria-hidden="true"
    >
      <path d="M12 3a6.5 6.5 0 1 0 9 9 8 8 0 1 1-9-9" />
    </svg>
  </button>
</template>
