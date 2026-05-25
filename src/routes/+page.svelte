<script lang="ts">
  import type { Picture } from '@sveltejs/enhanced-img';

  const imageModules = import.meta.glob('$lib/images/*.{jpg,jpeg}', {
    eager: true,
    query: '?enhanced',
  });

  const profileModules = import.meta.glob('$lib/images/profile.{jpg,jpeg}', {
    eager: true,
    query: '?enhanced',
  });

  let profileSrc = $derived(
    (Object.values(profileModules)[0] as { default: Picture } | undefined)?.default ?? null
  );

  let images = $derived(
    Object.entries(imageModules)
      .filter(([path]) => !path.toLowerCase().includes('/profile.'))
      .map(([path, mod]) => ({
        src: (mod as { default: Picture }).default,
        name: path.split('/').pop()?.replace(/\.jpe?g$/i, '') ?? 'shoe',
      }))
  );
</script>

<header class="fixed inset-x-0 top-0 z-50 border-b border-[#e5e5e5] bg-white/95 backdrop-blur-sm">
  <div class="mx-auto flex max-w-7xl items-center justify-between px-6 py-4">
    <div class="flex items-baseline gap-2">
      <h1 class="text-lg font-semibold tracking-tight text-[#111]">ShivaShakti</h1>
      <span class="text-xs font-medium tracking-widest text-[#555] uppercase">Collection</span>
    </div>
    <div class="hidden items-center gap-4 text-xs text-[#555] sm:flex">
      <span class="font-medium">ILAM, Nepal</span>
      <span class="h-3 w-px bg-[#e5e5e5]"></span>
      <span class="tracking-wide">info@shivashakti.com</span>
    </div>
  </div>
</header>

<main class="mx-auto max-w-7xl px-6 pt-24 pb-20">
  <section class="border-b border-[#e5e5e5] pb-12 pt-10 sm:pb-16">
    <div class="flex flex-col items-center gap-6 sm:flex-row sm:gap-8">
      <div class="shrink-0">
        {#if profileSrc}
          <div class="h-20 w-20 overflow-hidden rounded-full border-2 border-[#111] sm:h-24 sm:w-24">
            <enhanced:img src={profileSrc} alt="Profile" class="h-full w-full object-cover" />
          </div>
        {:else}
          <div class="flex h-20 w-20 items-center justify-center rounded-full border-2 border-dashed border-[#e5e5e5] bg-[#f5f5f5] sm:h-24 sm:w-24">
            <span class="text-[10px] font-medium tracking-wider text-[#555] uppercase">Profile</span>
          </div>
        {/if}
      </div>
      <div class="flex-1 text-center sm:text-left">
        <p class="text-sm font-medium tracking-widest text-[#555] uppercase">Curated footwear</p>
        <h2 class="mt-1 text-2xl font-semibold tracking-tight text-[#111] sm:text-3xl">
          Where every step tells a story
        </h2>
        <div class="mt-3 flex flex-col items-center gap-1 text-sm text-[#555] sm:items-start">
          <span>Ilam, Nepal</span>
          <span>info@shivashakticollection.com</span>
        </div>
        <div class="mt-4 flex items-center justify-center gap-5 sm:justify-start">
          <a
            href="https://facebook.com"
            target="_blank"
            rel="noopener noreferrer"
            class="flex items-center gap-2 text-sm font-medium text-[#555] transition hover:text-[#111]"
            aria-label="Facebook"
          >
            <svg class="h-5 w-5" fill="currentColor" viewBox="0 0 24 24">
              <path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/>
            </svg>
            Facebook
          </a>
          <a
            href="https://instagram.com"
            target="_blank"
            rel="noopener noreferrer"
            class="flex items-center gap-2 text-sm font-medium text-[#555] transition hover:text-[#111]"
            aria-label="Instagram"
          >
            <svg class="h-5 w-5" fill="currentColor" viewBox="0 0 24 24">
              <path d="M12 0C8.74 0 8.333.015 7.053.072 5.775.132 4.905.333 4.14.63c-.789.306-1.459.717-2.126 1.384S.935 3.35.63 4.14C.333 4.905.131 5.775.072 7.053.012 8.333 0 8.74 0 12s.015 3.667.072 4.947c.06 1.277.261 2.148.558 2.913.306.788.717 1.459 1.384 2.126.667.666 1.336 1.079 2.126 1.384.766.296 1.636.499 2.913.558C8.333 23.988 8.74 24 12 24s3.667-.015 4.947-.072c1.277-.06 2.148-.262 2.913-.558.788-.306 1.459-.718 2.126-1.384.666-.667 1.079-1.335 1.384-2.126.296-.765.499-1.636.558-2.913.06-1.28.072-1.687.072-4.947s-.015-3.667-.072-4.947c-.06-1.277-.262-2.149-.558-2.913-.306-.789-.718-1.459-1.384-2.126C21.319 1.347 20.651.935 19.86.63c-.765-.297-1.636-.499-2.913-.558C15.667.012 15.26 0 12 0zm0 2.16c3.203 0 3.585.016 4.85.071 1.17.055 1.805.249 2.227.415.562.217.96.477 1.382.896.419.42.679.819.896 1.381.164.422.36 1.057.413 2.227.057 1.266.07 1.646.07 4.85s-.015 3.585-.074 4.85c-.061 1.17-.256 1.805-.421 2.227-.224.562-.479.96-.899 1.382-.419.419-.824.679-1.38.896-.42.164-1.065.36-2.235.413-1.274.057-1.649.07-4.859.07-3.211 0-3.586-.015-4.859-.074-1.171-.061-1.816-.256-2.236-.421-.569-.224-.96-.479-1.379-.899-.421-.419-.69-.824-.9-1.38-.165-.42-.359-1.065-.42-2.235-.045-1.26-.061-1.649-.061-4.844 0-3.196.016-3.586.061-4.861.061-1.17.255-1.814.42-2.234.21-.57.479-.96.9-1.381.419-.419.81-.689 1.379-.898.42-.166 1.051-.361 2.221-.421 1.275-.045 1.65-.06 4.859-.06l.045.03zm0 3.678c-3.405 0-6.162 2.76-6.162 6.162 0 3.405 2.76 6.162 6.162 6.162 3.405 0 6.162-2.76 6.162-6.162 0-3.405-2.76-6.162-6.162-6.162zM12 16c-2.21 0-4-1.79-4-4s1.79-4 4-4 4 1.79 4 4-1.79 4-4 4zm7.846-10.405c0 .795-.646 1.44-1.44 1.44-.795 0-1.44-.646-1.44-1.44 0-.794.646-1.439 1.44-1.439.793-.001 1.44.645 1.44 1.439z"/>
            </svg>
            Instagram
          </a>
        </div>
      </div>
    </div>
  </section>

  <section class="pt-12">
    {#if images.length === 0}
      <div class="flex flex-col items-center justify-center py-24 text-[#555]">
        <svg class="mb-4 h-12 w-12" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
          <path stroke-linecap="round" stroke-linejoin="round" d="m2.25 15.75 5.159-5.159a2.25 2.25 0 0 1 3.182 0l5.159 5.159m-1.5-1.5 1.409-1.41a2.25 2.25 0 0 1 3.182 0l2.909 2.91m-18 3.75h16.5a1.5 1.5 0 0 0 1.5-1.5V6a1.5 1.5 0 0 0-1.5-1.5H3.75A1.5 1.5 0 0 0 2.25 6v12a1.5 1.5 0 0 0 1.5 1.5Zm10.5-11.25h.008v.008h-.008V8.25Zm.375 0a.375.375 0 1 1-.75 0 .375.375 0 0 1 .75 0Z" />
        </svg>
        <p class="text-sm font-medium">Drop your <span class="font-mono text-xs">.jpg</span> images in</p>
        <code class="mt-1 rounded-sm bg-[#f5f5f5] px-2 py-0.5 font-mono text-xs text-[#555]">src/lib/images/</code>
      </div>
    {:else}
      <div class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4">
        {#each images as { src, name } (src)}
          <div class="group relative aspect-[3/4] overflow-hidden rounded-sm bg-[#f5f5f5]">
            <enhanced:img
              src={src}
              alt={name}
              class="h-full w-full object-cover transition duration-700 group-hover:scale-105"
              loading="lazy"
            />
            <div class="pointer-events-none absolute inset-x-0 bottom-0 bg-gradient-to-t from-[#111]/60 to-transparent p-4 pt-12 opacity-0 transition duration-500 group-hover:opacity-100">
              <span class="text-xs font-medium tracking-wider text-white uppercase">{name}</span>
            </div>
          </div>
        {/each}
      </div>
    {/if}
  </section>
</main>

<footer class="border-t border-[#e5e5e5] bg-white">
  <div class="mx-auto flex max-w-7xl flex-col items-center gap-6 px-6 py-10 sm:flex-row sm:justify-between">
    <p class="text-xs font-medium tracking-wider text-[#555] uppercase">&copy; ShivaShakti Collection</p>
    <div class="flex items-center gap-5">
      <a
        href="https://facebook.com"
        target="_blank"
        rel="noopener noreferrer"
        class="text-sm font-medium text-[#555] transition hover:text-[#111]"
        aria-label="Facebook"
      >Facebook</a>
      <a
        href="https://instagram.com"
        target="_blank"
        rel="noopener noreferrer"
        class="text-sm font-medium text-[#555] transition hover:text-[#111]"
        aria-label="Instagram"
      >Instagram</a>
    </div>
  </div>
</footer>
