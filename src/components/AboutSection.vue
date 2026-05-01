<template>
  <section id="about" class="about section-pad">
    <div class="container">
      <div class="section-label">
        <span class="label-num">01</span>
        <span class="label-line"></span>
        <span class="label-text">About</span>
      </div>
      <div class="about-grid">
        <div class="about-text">
          <h2 class="section-title">About Me<br /><em>experiences</em></h2>
          <p>
            Frontend Web Developer with over 2+ year of experience building responsive, accessible,
            and user-centric web applications, primarily in the government and public service
            sector. Proficient in Vue.js, Vuetify, Tailwind CSS, Vuex, and Axios, with a strong
            understanding of component-based architecture and API integration. Passionate about
            creating clean, intuitive UIs that improve user experience and streamline digital
            workflows.
          </p>
          <div class="skills-grid">
            <div class="skill-group" v-for="group in skillGroups" :key="group.title">
              <p class="skill-group-title">{{ group.title }}</p>
              <ul>
                <li v-for="skill in group.skills" :key="skill">
                  <span class="skill-arrow">▸</span> {{ skill }}
                </li>
              </ul>
            </div>
          </div>
        </div>
        <div class="about-visual">
          <div class="avatar-frame">
            <div class="avatar-placeholder">
              <span>D</span>
            </div>
            <div class="frame-deco frame-deco-1"></div>
            <div class="frame-deco frame-deco-2"></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
const skillGroups = [
  {
    title: 'Frontend',
    skills: ['Vue / Nuxt', 'React Native', 'TypeScript', 'JavaSript', 'Tailwind CSS', 'Vuetify'],
  },
  // {
  //   title: 'Backend',
  //   skills: ['Node.js / Express', 'Laravel / PHP', 'PostgreSQL', 'REST APIs'],
  // },
  {
    title: 'Tools',
    skills: ['Git', 'Postman', 'Figma', 'Bitbucket'],
  },
]
</script>

<style scoped>
.section-pad {
  padding: 8rem 2rem;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.section-label {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 4rem;
}

.label-num {
  font-size: 0.7rem;
  color: var(--accent);
  letter-spacing: 0.1em;
}

.label-line {
  flex: 0 0 60px;
  height: 1px;
  background: var(--border);
}

.label-text {
  font-size: 0.7rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--text-muted);
}

.about-grid {
  display: grid;
  grid-template-columns: 1fr 380px;
  gap: 6rem;
  align-items: center;
}

.section-title {
  font-family: var(--font-display);
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 700;
  line-height: 1.05;
  margin-bottom: 2rem;
  letter-spacing: -0.02em;
}

.section-title em {
  font-style: italic;
  color: var(--accent);
}

.about-text p {
  color: var(--text-muted);
  margin-bottom: 1.25rem;
  font-size: 0.95rem;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  margin-top: 2.5rem;
  padding-top: 2.5rem;
  border-top: 1px solid var(--border);
}

.skill-group-title {
  font-size: 0.65rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 0.75rem;
}

.skill-group ul {
  list-style: none;
}

.skill-group li {
  font-size: 0.8rem;
  color: var(--text-muted);
  padding: 0.2rem 0;
  display: flex;
  align-items: center;
  gap: 0.4rem;
}

.skill-arrow {
  color: var(--accent);
  font-size: 0.6rem;
}

.about-visual {
  display: flex;
  justify-content: center;
}

.avatar-frame {
  position: relative;
  width: 320px;
  height: 380px;
}

.avatar-placeholder {
  width: 100%;
  height: 100%;
  background: var(--bg-3);
  border: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-display);
  font-size: 8rem;
  font-weight: 900;
  color: var(--accent);
  position: relative;
  z-index: 1;
}

.frame-deco {
  position: absolute;
  border: 1px solid var(--accent);
  opacity: 0.3;
}

.frame-deco-1 {
  width: 100%;
  height: 100%;
  top: 12px;
  left: 12px;
}

.frame-deco-2 {
  width: 60px;
  height: 60px;
  bottom: -20px;
  right: -20px;
  background: var(--accent);
  opacity: 0.15;
}

@media (max-width: 900px) {
  .about-grid {
    grid-template-columns: 1fr;
  }
  .about-visual {
    display: none;
  }
  .skills-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>
