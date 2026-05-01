<template>
  <nav class="navbar" :class="{ scrolled: isScrolled }">
    <div class="nav-inner">
      <a href="#hero" class="nav-logo">
        <span class="logo-bracket">[</span>
        <span class="logo-name">Daniel</span>
        <span class="logo-bracket">]</span>
      </a>

      <ul class="nav-links">
        <li v-for="link in links" :key="link.href">
          <a :href="link.href" class="nav-link">
            <span class="link-num">{{ link.num }}</span>
            {{ link.label }}
          </a>
        </li>
      </ul>

      <a href="mailto:daniel@email.com" class="nav-cta">Hire Me</a>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)

const links = [
  { href: '#about', label: 'About', num: '01' },
  { href: '#experience', label: 'Experience', num: '02' },
  { href: '#projects', label: 'Projects', num: '03' },
  { href: '#contact', label: 'Contact', num: '04' },
]

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  padding: 1.5rem 2rem;
  transition: all 0.4s ease;
}

.navbar.scrolled {
  background: rgba(10, 10, 10, 0.92);
  backdrop-filter: blur(12px);
  padding: 1rem 2rem;
  border-bottom: 1px solid var(--border);
}

.nav-inner {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav-logo {
  font-family: var(--font-display);
  font-size: 1.25rem;
  font-weight: 700;
  letter-spacing: 0.05em;
}

.logo-bracket {
  color: var(--accent);
}

.nav-links {
  display: flex;
  gap: 2.5rem;
  list-style: none;
}

.nav-link {
  font-size: 0.75rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--text-muted);
  transition: color 0.3s;
  display: flex;
  align-items: center;
  gap: 0.4rem;
}

.nav-link:hover {
  color: var(--text);
}

.link-num {
  color: var(--accent);
  font-size: 0.65rem;
}

.nav-cta {
  font-size: 0.7rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  border: 1px solid var(--accent);
  color: var(--accent);
  padding: 0.5rem 1.25rem;
  transition: all 0.3s;
}

.nav-cta:hover {
  background: var(--accent);
  color: var(--bg);
}

@media (max-width: 768px) {
  .nav-links { display: none; }
}
</style>