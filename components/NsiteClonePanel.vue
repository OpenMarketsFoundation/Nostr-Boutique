<script setup>
const {
  defaultSourceNpub,
  defaultRelays,
  generateIdentity,
  fetchSourceManifest,
  publishProfile,
  publishClonedManifest,
  publishClonedManifestWithExtension
} = useNsiteClone()

const sourceNpub = defaultSourceNpub

const mode = ref('idle')

const existingBusy = ref(false)
const existingError = ref('')
const existingSuccessUrl = ref('')

const newcomerName = ref('')
const newcomerIdentity = ref(null)
const newcomerConfirmed = ref(false)
const newcomerBusy = ref(false)
const newcomerError = ref('')
const newcomerSuccessUrl = ref('')

const copyText = async (value) => {
  if (!process.client || !value) return
  await navigator.clipboard.writeText(value)
}

const resetStatus = () => {
  existingError.value = ''
  existingSuccessUrl.value = ''
  newcomerError.value = ''
  newcomerSuccessUrl.value = ''
}

const runExistingFlow = async () => {
  mode.value = 'existing'
  resetStatus()
  existingBusy.value = true

  try {
    const source = await fetchSourceManifest({
      sourceNpub,
      relays: defaultRelays
    })

    const publishRelays = source.manifestRelays.length > 0 ? source.manifestRelays : defaultRelays

    const result = await publishClonedManifestWithExtension({
      sourceManifest: source.manifest,
      sourcePubkey: source.sourcePubkey,
      relays: publishRelays
    })

    const siteUrl = `https://${result.npub}.nsite.lol/`
    existingSuccessUrl.value = siteUrl

    if (process.client) {
      const opened = window.open(siteUrl, '_blank', 'noopener,noreferrer')
      if (!opened) existingError.value = 'Clone published, but your browser blocked opening a new tab.'
    }

    mode.value = 'existing-success'
  } catch (error) {
    existingError.value = error.message || 'Could not clone with your current signer.'
  } finally {
    existingBusy.value = false
  }
}

const startNewcomerFlow = () => {
  mode.value = 'new'
  resetStatus()
}

const generateNewcomerKeys = () => {
  newcomerIdentity.value = generateIdentity()
  newcomerConfirmed.value = false
  newcomerError.value = ''
}

const runNewcomerFlow = async () => {
  newcomerError.value = ''

  if (!newcomerName.value.trim()) {
    newcomerError.value = 'Please enter a display name.'
    return
  }

  if (!newcomerIdentity.value) {
    newcomerError.value = 'Generate your keys first.'
    return
  }

  if (!newcomerConfirmed.value) {
    newcomerError.value = 'Please confirm that you backed up your keys.'
    return
  }

  newcomerBusy.value = true

  try {
    const source = await fetchSourceManifest({
      sourceNpub,
      relays: defaultRelays
    })

    const publishRelays = source.manifestRelays.length > 0 ? source.manifestRelays : defaultRelays

    await publishProfile({
      identity: newcomerIdentity.value,
      name: newcomerName.value.trim(),
      relays: publishRelays
    })

    await publishClonedManifest({
      identity: newcomerIdentity.value,
      sourceManifest: source.manifest,
      sourcePubkey: source.sourcePubkey,
      relays: publishRelays
    })

    const siteUrl = `https://${newcomerIdentity.value.npub}.nsite.lol/`
    newcomerSuccessUrl.value = siteUrl

    if (process.client) {
      const opened = window.open(siteUrl, '_blank', 'noopener,noreferrer')
      if (!opened) newcomerError.value = 'Clone published, but your browser blocked opening a new tab.'
    }

    mode.value = 'new-success'
  } catch (error) {
    newcomerError.value = error.message || 'Failed to publish your profile and clone.'
  } finally {
    newcomerBusy.value = false
  }
}
</script>

<template>
  <div class="mx-auto mt-10 grid max-w-xl gap-3 sm:grid-cols-2">
    <button
      class="cta-primary inline-flex items-center justify-center border px-6 py-3 text-sm font-bold transition hover:opacity-90 disabled:opacity-70"
      :disabled="existingBusy || newcomerBusy"
      @click="runExistingFlow"
    >
      {{ existingBusy ? 'Cloning...' : 'I have a key' }}
    </button>

    <button
      class="cta-accent inline-flex items-center justify-center border px-6 py-3 text-sm font-bold transition hover:opacity-80"
      :disabled="existingBusy || newcomerBusy"
      @click="startNewcomerFlow"
    >
      I'm new here
    </button>
  </div>

  <div v-if="existingError" class="mx-auto mt-4 max-w-xl border border-red-500/40 px-4 py-3 text-sm text-red-500">
    {{ existingError }}
  </div>

  <div v-if="mode === 'existing-success'" class="mx-auto mt-4 max-w-xl border px-4 py-3 text-sm" :style="{ borderColor: 'var(--line)' }">
    <p class="font-bold">Clone published with your key.</p>
    <a class="mt-2 inline-block underline" :href="existingSuccessUrl" target="_blank" rel="noopener noreferrer">{{ existingSuccessUrl }}</a>
  </div>

  <div v-if="mode === 'new' || mode === 'new-success'" class="mx-auto mt-6 max-w-xl border p-4" :style="{ borderColor: 'var(--line)' }">
    <p class="text-sm font-bold">Clone source</p>
    <p class="mt-1 break-all text-xs" :style="{ color: 'var(--muted)' }">{{ sourceNpub }}</p>

    <label class="mt-4 block text-xs font-bold uppercase tracking-[0.08em]" :style="{ color: 'var(--muted)' }">Display name</label>
    <input
      v-model="newcomerName"
      type="text"
      placeholder="Sovereign Shop Owner"
      class="mt-2 w-full border px-3 py-2 text-sm outline-none"
      :style="{ borderColor: 'var(--line)', background: 'var(--bg)', color: 'var(--text)' }"
    >

    <div class="mt-3 flex flex-wrap gap-2">
      <button class="border px-3 py-2 text-xs font-bold" :style="{ borderColor: 'var(--line)' }" @click="generateNewcomerKeys">
        Generate my keys
      </button>
    </div>

    <div v-if="newcomerIdentity" class="mt-4 border p-3 text-xs" :style="{ borderColor: 'var(--line)' }">
      <p class="font-bold">Back up these keys now.</p>
      <p class="mt-2 break-all"><span class="font-bold">npub:</span> {{ newcomerIdentity.npub }}</p>
      <p class="mt-1 break-all"><span class="font-bold">nsec:</span> {{ newcomerIdentity.nsec }}</p>
      <div class="mt-2 flex flex-wrap gap-2">
        <button class="border px-2 py-1" :style="{ borderColor: 'var(--line)' }" @click="copyText(newcomerIdentity.npub)">Copy npub</button>
        <button class="border px-2 py-1" :style="{ borderColor: 'var(--line)' }" @click="copyText(newcomerIdentity.nsec)">Copy nsec</button>
      </div>
      <label class="mt-3 flex items-center gap-2">
        <input v-model="newcomerConfirmed" type="checkbox">
        <span>I saved my keys securely.</span>
      </label>

      <button
        class="cta-primary mt-3 border px-3 py-2 text-xs font-bold disabled:opacity-70"
        :disabled="newcomerBusy"
        @click="runNewcomerFlow"
      >
        {{ newcomerBusy ? 'Publishing...' : 'Publish profile and clone' }}
      </button>
    </div>

    <p v-if="newcomerError" class="mt-3 text-xs text-red-500">{{ newcomerError }}</p>

    <div v-if="mode === 'new-success'" class="mt-4 border p-3 text-xs" :style="{ borderColor: 'var(--line)' }">
      <p class="font-bold">Your new nsite is live.</p>
      <a class="mt-2 inline-block underline" :href="newcomerSuccessUrl" target="_blank" rel="noopener noreferrer">{{ newcomerSuccessUrl }}</a>
    </div>
  </div>
</template>
