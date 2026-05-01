<template>
  <div class="app">
    <NavBar />
    <RouterView />
  </div>
</template>

<script setup lang="ts">
import NavBar from './components/NavBar.vue'
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400&family=DM+Mono:wght@300;400;500&display=swap');

*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

:root {
  --bg: #0a0a0a;
  --bg-2: #111111;
  --bg-3: #1a1a1a;
  --text: #f0ece4;
  --text-muted: #7a7570;
  --accent: #c8a96e;
  --accent-2: #e8c98e;
  --border: rgba(200, 169, 110, 0.15);
  --font-display: 'Playfair Display', Georgia, serif;
  --font-mono: 'DM Mono', monospace;
}

html {
  scroll-behavior: smooth;
}

body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--font-mono);
  font-weight: 300;
  line-height: 1.7;
  overflow-x: hidden;
}

::selection {
  background: var(--accent);
  color: var(--bg);
}

::-webkit-scrollbar {
  width: 4px;
}
::-webkit-scrollbar-track {
  background: var(--bg);
}
::-webkit-scrollbar-thumb {
  background: var(--accent);
  border-radius: 2px;
}

a {
  color: inherit;
  text-decoration: none;
}
</style>