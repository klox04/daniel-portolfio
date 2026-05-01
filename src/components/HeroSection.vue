<template>
  <section id="hero" class="hero">
    <div class="hero-bg-grid"></div>
    <div class="hero-content">
      <p class="hero-tag">
        <span class="dot"></span>
        Available for work
      </p>
      <h1 class="hero-title">
        <span class="title-line">Daniel</span>
        <span class="title-line italic">Portfolio</span>
      </h1>
      <p class="hero-role">Fron-end Developer </p>
      <p class="hero-desc">
        Hi, I'm Daniel — a frontend developer who loves building clean and responsive websites. 
         I enjoy turning designs into real, working interfaces that look good and feel smooth to use.
      </p>
      <div class="hero-actions">
        <a href="#projects" class="btn-primary">View Projects</a>
        <a href="#experience" class="btn-ghost">My Experience</a>
      </div>
    </div>

    <div class="hero-side">
      <div class="side-stat" v-for="stat in stats" :key="stat.label">
        <span class="stat-num">{{ stat.value }}</span>
        <span class="stat-label">{{ stat.label }}</span>
      </div>
    </div>

    <div class="scroll-hint">
      <span>scroll</span>
      <div class="scroll-line"></div>
    </div>
  </section>
</template>

<script setup lang="ts">
const stats = [
  { value: '2+', label: 'Years Experience' },
  { value: '5+', label: 'Projects Shipped' },
//   { value: '5+', label: 'Happy Clients' },
]
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: 8rem 2rem 4rem;
  position: relative;
  overflow: hidden;
  max-width: 1200px;
  margin: 0 auto;
}

.hero-bg-grid {
  position: fixed;
  inset: 0;
  background-image:
    linear-gradient(rgba(200,169,110,0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(200,169,110,0.03) 1px, transparent 1px);
  background-size: 80px 80px;
  pointer-events: none;
  z-index: -1;
}

.hero-content {
  flex: 1;
  max-width: 680px;
}

.hero-tag {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  font-size: 0.72rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 2rem;
}

.dot {
  width: 6px;
  height: 6px;
  background: var(--accent);
  border-radius: 50%;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.4; transform: scale(1.5); }
}

.hero-title {
  font-family: var(--font-display);
  font-size: clamp(4rem, 10vw, 8rem);
  font-weight: 900;
  line-height: 0.9;
  margin-bottom: 1.5rem;
  letter-spacing: -0.02em;
}

.title-line {
  display: block;
}

.italic {
  font-style: italic;
  color: transparent;
  -webkit-text-stroke: 1px var(--accent);
}

.hero-role {
  font-size: 0.85rem;
  letter-spacing: 0.1em;
  color: var(--text-muted);
  text-transform: uppercase;
  margin-bottom: 1.5rem;
}

.sep {
  color: var(--accent);
  margin: 0 0.5rem;
}

.hero-desc {
  font-size: 1rem;
  color: var(--text-muted);
  max-width: 460px;
  margin-bottom: 3rem;
  line-height: 1.8;
}

.hero-actions {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.btn-primary {
  background: var(--accent);
  color: var(--bg);
  padding: 0.85rem 2rem;
  font-family: var(--font-mono);
  font-size: 0.75rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  transition: all 0.3s;
}

.btn-primary:hover {
  background: var(--accent-2);
}

.btn-ghost {
  border: 1px solid var(--border);
  color: var(--text-muted);
  padding: 0.85rem 2rem;
  font-family: var(--font-mono);
  font-size: 0.75rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  transition: all 0.3s;
}

.btn-ghost:hover {
  border-color: var(--accent);
  color: var(--accent);
}

.hero-side {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
  padding-left: 4rem;
  border-left: 1px solid var(--border);
}

.side-stat {
  display: flex;
  flex-direction: column;
}

.stat-num {
  font-family: var(--font-display);
  font-size: 2.5rem;
  font-weight: 700;
  color: var(--accent);
  line-height: 1;
}

.stat-label {
  font-size: 0.7rem;
  letter-spacing: 0.1em;
  color: var(--text-muted);
  text-transform: uppercase;
  margin-top: 0.25rem;
}

.scroll-hint {
  position: absolute;
  bottom: 3rem;
  left: 2rem;
  display: flex;
  align-items: center;
  gap: 1rem;
  font-size: 0.65rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--text-muted);
  writing-mode: vertical-rl;
}

.scroll-line {
  width: 1px;
  height: 60px;
  background: linear-gradient(to bottom, var(--accent), transparent);
  animation: scrollAnim 2s ease-in-out infinite;
}

@keyframes scrollAnim {
  0% { transform: scaleY(0); transform-origin: top; }
  50% { transform: scaleY(1); transform-origin: top; }
  51% { transform: scaleY(1); transform-origin: bottom; }
  100% { transform: scaleY(0); transform-origin: bottom; }
}

@media (max-width: 768px) {
  .hero-side { display: none; }
  .hero { padding-top: 6rem; }
}
</style>