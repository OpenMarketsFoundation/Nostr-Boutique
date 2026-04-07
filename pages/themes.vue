<script setup>
import themesData from '~/data/themes.json'

const {
  defaultRelays,
  fetchSourceManifest,
  publishClonedManifestWithExtension
} = useNsiteClone()

useSeoMeta({
  title: 'Themes | Nostr Boutique',
  description: 'Clone-ready nsite themes loaded from a local JSON file.'
})

const defaultThemeImage = 'https://raw.githubusercontent.com/S7NC/Gamma-Napp/master/public/screenshot.png'

const themes = computed(() => {
  if (!Array.isArray(themesData)) return []
  return themesData
})

const busyByTheme = ref({})
const errorByTheme = ref({})
const successByTheme = ref({})

const themeKey = (theme) => theme.id || `${theme.npub}-${theme.d || 'root'}`

const toGatewayUrls = (theme) => {
  const npub = theme.npub
  return {
    cloud: `https://${npub}.nsite.cloud/`,
    run: `https://${npub}.nsite.run/`,
    lol: `https://${npub}.nsite.lol/`
  }
}

const setBusy = (key, value) => {
  busyByTheme.value = {
    ...busyByTheme.value,
    [key]: value
  }
}

const setError = (key, value) => {
  errorByTheme.value = {
    ...errorByTheme.value,
    [key]: value
  }
}

const setSuccess = (key, value) => {
  successByTheme.value = {
    ...successByTheme.value,
    [key]: value
  }
}

const cloneTheme = async (theme) => {
  const key = themeKey(theme)
  setError(key, '')
  setSuccess(key, '')

  if (!process.client || !window.nostr || typeof window.nostr.getPublicKey !== 'function' || typeof window.nostr.signEvent !== 'function') {
    setError(key, 'Browser signer extension required (NIP-07).')
    return
  }

  setBusy(key, true)
  const pendingWindow = window.open('', '_blank')

  try {
    const source = await fetchSourceManifest({
      sourceNpub: theme.npub,
      relays: defaultRelays,
      siteType: theme.cloneAs === 'named' ? 'named' : 'root',
      namedSiteKey: theme.cloneAs === 'named' ? (theme.d || '') : ''
    })

    const publishRelays = source.manifestRelays.length > 0 ? source.manifestRelays : defaultRelays

    const result = await publishClonedManifestWithExtension({
      sourceManifest: source.manifest,
      sourcePubkey: source.sourcePubkey,
      relays: publishRelays,
      cloneAs: theme.cloneAs === 'named' ? 'named' : 'root',
      namedSiteKey: theme.cloneAs === 'named' ? (theme.d || '') : ''
    })

    const url = `https://${result.npub}.nsite.cloud/`
    setSuccess(key, url)

    if (pendingWindow) {
      pendingWindow.location.href = url
    } else {
      const opened = window.open(url, '_blank', 'noopener,noreferrer')
      if (!opened) setError(key, 'Clone published, but your browser blocked opening a new tab.')
    }
  } catch (error) {
    if (pendingWindow && !pendingWindow.closed) pendingWindow.close()
    setError(key, error.message || 'Could not clone this theme with your signer.')
  } finally {
    setBusy(key, false)
  }
}
</script>

<template>
  <section class="fade-in-up">
    <div class="surface-card p-6 sm:p-8">
      <h1 class="text-3xl font-black sm:text-4xl">Themes</h1>
    </div>
  </section>

  <section class="mt-6">
    <div v-if="themes.length === 0" class="border px-4 py-3 text-sm" :style="{ borderColor: 'var(--line)' }">
      No themes listed yet.
    </div>

    <div v-else class="grid gap-4 md:grid-cols-2 xl:grid-cols-3">
      <article v-for="theme in themes" :key="themeKey(theme)" class="surface-card p-5">
        <img
          :src="theme.image || defaultThemeImage"
          :alt="`${theme.title || 'Theme'} preview`"
          class="mb-4 w-full rounded-xl border"
          :style="{ borderColor: 'var(--line)' }"
          loading="lazy"
        >

        <p class="text-xs font-bold uppercase tracking-[0.08em]" :style="{ color: 'var(--muted)' }">
          {{ theme.cloneAs === 'named' ? 'Named clone' : 'Root clone' }}
        </p>
        <h2 class="mt-2 text-lg font-black">{{ theme.title || 'Untitled theme' }}</h2>
        <p v-if="theme.description" class="mt-2 text-sm" :style="{ color: 'var(--muted)' }">{{ theme.description }}</p>

        <p class="mt-3 break-all text-xs" :style="{ color: 'var(--muted)' }">{{ theme.npub }}</p>
        <p v-if="theme.cloneAs === 'named' && theme.d" class="mt-1 text-xs" :style="{ color: 'var(--muted)' }">
          d tag: <code>{{ theme.d }}</code>
        </p>

        <div class="mt-3 flex items-center gap-2">
          <a
            :href="toGatewayUrls(theme).cloud"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex h-9 w-9 items-center justify-center rounded-full border text-base"
            :style="{ borderColor: 'var(--line)' }"
            aria-label="Open template via nsite.cloud"
            title="Open template via nsite.cloud"
          >
            ⛅️
          </a>
          <a
            :href="toGatewayUrls(theme).run"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex h-9 w-9 items-center justify-center rounded-full border text-base"
            :style="{ borderColor: 'var(--line)' }"
            aria-label="Open template via nsite.run"
            title="Open template via nsite.run"
          >
            🏃
          </a>
          <a
            :href="toGatewayUrls(theme).lol"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex h-9 w-9 items-center justify-center rounded-full border text-base"
            :style="{ borderColor: 'var(--line)' }"
            aria-label="Open template via nsite.lol"
            title="Open template via nsite.lol"
          >
            😂
          </a>
        </div>

        <button
          type="button"
          class="mt-4 inline-flex items-center justify-center rounded-xl border px-4 py-2.5 text-xs font-black uppercase tracking-[0.08em] transition disabled:opacity-60"
          :style="{ borderColor: '#8b5cf6', background: 'linear-gradient(90deg, #7c3aed 0%, #a855f7 100%)', color: '#fff' }"
          :disabled="busyByTheme[themeKey(theme)]"
          @click="cloneTheme(theme)"
        >
          {{ busyByTheme[themeKey(theme)] ? 'Cloning...' : 'Clone this theme' }}
        </button>

        <p v-if="errorByTheme[themeKey(theme)]" class="mt-3 text-xs text-red-500">{{ errorByTheme[themeKey(theme)] }}</p>
        <a
          v-if="successByTheme[themeKey(theme)]"
          :href="successByTheme[themeKey(theme)]"
          target="_blank"
          rel="noopener noreferrer"
          class="mt-3 inline-block text-xs underline"
        >
          {{ successByTheme[themeKey(theme)] }}
        </a>

        <p class="mt-2 text-xs" :style="{ color: 'var(--muted)' }">
          Requires browser extension signer.
        </p>
      </article>
    </div>
  </section>
</template>
