<script lang="ts">
  import '../app.css';
  import { theme } from '$lib/stores/theme';
  import { onMount } from 'svelte';
  
  let { children } = $props();
  
  onMount(() => {
    if ($theme === 'dark') {
      document.documentElement.classList.add('dark');
    }
  });

  function toggleTheme() {
    theme.update(current => {
      const newTheme = current === 'light' ? 'dark' : 'light';
      document.documentElement.classList.toggle('dark');
      return newTheme;
    });
  }
</script>

<div class="min-h-screen">
  <header class="fixed top-0 z-50 w-full bg-white shadow-md dark:bg-gray-800">
    <nav class="container mx-auto px-4 py-4">
      <div class="flex items-center justify-between">
        <a href="/" class="text-2xl font-bold text-primary-600">WebDev Co.</a>
        <div class="flex items-center gap-4">
          <a href="/services" class="hover:text-primary-600">Services</a>
          <a href="/portfolio" class="hover:text-primary-600">Portfolio</a>
          <a href="/contact" class="hover:text-primary-600">Contact</a>
          <button
            on:click={toggleTheme}
            class="rounded-full p-2 hover:bg-gray-100 dark:hover:bg-gray-700"
          >
            {#if $theme === 'light'}
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
              </svg>
            {:else}
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707" />
              </svg>
            {/if}
          </button>
        </div>
      </div>
    </nav>
  </header>

  <main class="container mx-auto px-4 pt-24">
    {@render children()}
  </main>

  <footer class="mt-16 bg-gray-100 py-8 dark:bg-gray-800">
    <div class="container mx-auto px-4 text-center">
      <p>&copy; 2024 WebDev Co. All rights reserved.</p>
    </div>
  </footer>
</div>
