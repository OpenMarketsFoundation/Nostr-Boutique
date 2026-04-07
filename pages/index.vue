<script setup>
useSeoMeta({
  title: 'Nostr Boutique',
  description: 'Host your own self sovereign shop.'
})
</script>

<template>
  <section class="w-full pb-14 text-center sm:pb-20">
    <div
      class="hero-panel relative w-full overflow-hidden bg-cover bg-center px-4 py-8 sm:px-8 sm:py-10"
    >
      <div class="mx-auto max-w-3xl">
        <NsiteClonePanel />
      </div>
    </div>

    <div class="mx-auto mt-8 w-full max-w-7xl px-2 text-left md:px-4 lg:px-0">
      <h2 class="text-center text-2xl font-black sm:text-3xl">How it works</h2>
      <p class="mx-auto mt-2 max-w-2xl text-center text-sm" :style="{ color: 'var(--muted)' }">
        Launch and manage your sovereign storefront with open identity and portable infrastructure.
      </p>

      <div class="mt-6 grid grid-cols-1 gap-4 md:grid-cols-2 lg:grid-cols-4 lg:gap-6">
        <article class="overflow-hidden rounded-2xl border transition hover:-translate-y-0.5" :style="{ borderColor: 'var(--line)', background: 'var(--bg-soft)' }">
          <div class="border-b" :style="{ borderColor: 'var(--line)', background: 'color-mix(in oklab, var(--bg) 95%, var(--text) 5%)' }">
            <img src="/1.png" alt="Step 1" class="block h-36 w-full object-cover">
          </div>
          <div class="p-4">
            <h3 class="text-base font-black">The key is your identity</h3>
            <p class="mt-2 text-sm" :style="{ color: 'var(--muted)' }">Your Nostr keypair is your account and ownership layer.</p>
          </div>
        </article>

        <article class="overflow-hidden rounded-2xl border transition hover:-translate-y-0.5" :style="{ borderColor: 'var(--line)', background: 'var(--bg-soft)' }">
          <div class="border-b" :style="{ borderColor: 'var(--line)', background: 'color-mix(in oklab, var(--bg) 95%, var(--text) 5%)' }">
            <img src="/2.png" alt="Step 2" class="block h-36 w-full object-cover">
          </div>
          <div class="p-4">
            <h3 class="text-base font-black">Clone to multiple relays</h3>
            <p class="mt-2 text-sm" :style="{ color: 'var(--muted)' }">Publish your site manifest to multiple servers (relays) for reach and redundancy.</p>
          </div>
        </article>

        <article class="overflow-hidden rounded-2xl border transition hover:-translate-y-0.5" :style="{ borderColor: 'var(--line)', background: 'var(--bg-soft)' }">
          <div class="border-b" :style="{ borderColor: 'var(--line)', background: 'color-mix(in oklab, var(--bg) 95%, var(--text) 5%)' }">
            <img src="/3.png" alt="Step 3" class="block h-36 w-full object-cover">
          </div>
          <div class="p-4">
            <h3 class="text-base font-black">Open through multiple gateways</h3>
            <p class="mt-2 text-sm" :style="{ color: 'var(--muted)' }">Accessible via <code>npub*.nsite.cloud</code>, <code>npub*.nsite.lol</code>, and <code>npub*.nsite.run</code>.</p>
          </div>
        </article>

        <article class="overflow-hidden rounded-2xl border transition hover:-translate-y-0.5" :style="{ borderColor: 'var(--line)', background: 'var(--bg-soft)' }">
          <div class="border-b" :style="{ borderColor: 'var(--line)', background: 'color-mix(in oklab, var(--bg) 95%, var(--text) 5%)' }">
            <img src="/4.png" alt="Step 4" class="block h-36 w-full object-cover">
          </div>
          <div class="p-4">
            <h3 class="text-base font-black">Use multiple CMS clients</h3>
            <p class="mt-2 text-sm" :style="{ color: 'var(--muted)' }">Manage inventory with Plebeian.market, shopstr.store, and conduit.market.</p>
          </div>
        </article>
      </div>
    </div>

    <div class="mx-auto mt-8 w-full max-w-7xl px-4 sm:px-0">
      <div class="grid grid-cols-1 gap-3 md:grid-cols-2 lg:grid-cols-4">
        <article class="rounded-2xl border px-4 py-4 text-center" :style="{ borderColor: 'var(--line)', background: 'var(--bg-soft)' }">
          <p class="text-2xl">💳</p>
          <p class="mt-2 text-sm font-bold leading-6">No credit card or monthly fees!</p>
        </article>

        <article class="rounded-2xl border px-4 py-4 text-center" :style="{ borderColor: 'var(--line)', background: 'var(--bg-soft)' }">
          <p class="text-2xl">📵</p>
          <p class="mt-2 text-sm font-bold leading-6">No email address or phone number!</p>
        </article>

        <article class="rounded-2xl border px-4 py-4 text-center" :style="{ borderColor: 'var(--line)', background: 'var(--bg-soft)' }">
          <p class="text-2xl">⚡</p>
          <p class="mt-2 text-sm font-bold leading-6">As close to one-click deploy as possible.</p>
        </article>

        <article class="rounded-2xl border px-4 py-4 text-center" :style="{ borderColor: 'var(--line)', background: 'var(--bg-soft)' }">
          <p class="text-2xl">🛠️</p>
          <p class="mt-2 text-sm font-bold leading-6">No technical skills required.</p>
        </article>
      </div>

    </div>
  </section>
</template>
