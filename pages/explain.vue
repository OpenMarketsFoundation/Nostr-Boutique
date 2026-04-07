<script setup>
useSeoMeta({
  title: 'Explain | Nostr Boutique',
  description: 'Understand Nostr, Nsites, and gateways in plain language.'
})
</script>

<template>
  <section class="fade-in-up">
    <div class="surface-card p-6 sm:p-8">
      <span class="pill">Beginner friendly guide</span>
      <h1 class="hero-title mt-4 text-4xl font-black leading-tight">What are Nostr, Nsites, and gateways?</h1>
      <p class="mt-3 max-w-3xl text-sm sm:text-base" :style="{ color: 'var(--muted)' }">
        If you are new to this stack, this page gives the practical mental model for how a sovereign storefront appears online.
      </p>
    </div>
  </section>

  <section class="mt-6 grid gap-4 md:grid-cols-3">
    <article class="panel fade-in-up">
      <p class="text-xs font-extrabold uppercase tracking-[0.1em]" :style="{ color: 'var(--brand)' }">01</p>
      <h2 class="mt-2 text-xl font-black">Nostr</h2>
      <p class="mt-3 text-sm" :style="{ color: 'var(--muted)' }">
        Nostr is an open protocol for signed events. Your account is your keypair, not a username in one company database.
      </p>
    </article>

    <article class="panel fade-in-up">
      <p class="text-xs font-extrabold uppercase tracking-[0.1em]" :style="{ color: 'var(--brand)' }">02</p>
      <h2 class="mt-2 text-xl font-black">Nsite</h2>
      <p class="mt-3 text-sm" :style="{ color: 'var(--muted)' }">
        An Nsite is site content and metadata published over Nostr-compatible rails. It can be cloned to another key and updated without platform lock-in.
      </p>
    </article>

    <article class="panel fade-in-up">
      <p class="text-xs font-extrabold uppercase tracking-[0.1em]" :style="{ color: 'var(--brand)' }">03</p>
      <h2 class="mt-2 text-xl font-black">Gateway</h2>
      <p class="mt-3 text-sm" :style="{ color: 'var(--muted)' }">
        A gateway is the web-facing domain that resolves Nsite data into regular HTTP pages, such as <code>*.nsite.cloud</code>, <code>*.nsite.run</code>, and <code>*.nsite.lol</code>.
      </p>
    </article>
  </section>

  <section class="mt-6 grid gap-4 lg:grid-cols-[1.2fr_1fr]">
    <article class="surface-card p-6">
      <h2 class="text-2xl font-black">Simple flow</h2>
      <ol class="mt-4 space-y-2 text-sm" :style="{ color: 'var(--muted)' }">
        <li>1. Merchant controls a Nostr keypair.</li>
        <li>2. Merchant publishes storefront manifest and content pointers.</li>
        <li>3. Relays and servers distribute the data.</li>
        <li>4. Gateway resolves and renders the storefront for browsers.</li>
      </ol>
    </article>

    <article class="surface-card p-6">
      <h2 class="text-2xl font-black">Why it matters</h2>
      <ul class="mt-4 space-y-2 text-sm" :style="{ color: 'var(--muted)' }">
        <li>- Lower platform dependence.</li>
        <li>- Easier migration and cloning.</li>
        <li>- User-owned merchant identity.</li>
        <li>- Open ecosystem interoperability.</li>
      </ul>
      <NuxtLink to="/example" class="mt-5 inline-flex rounded-full border px-4 py-2 text-sm font-bold" :style="{ borderColor: 'var(--line)' }">
        See a live example
      </NuxtLink>
    </article>
  </section>
</template>
