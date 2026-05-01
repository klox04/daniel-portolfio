<template>
  <section id="experience" class="experience section-pad">
    <div class="container">
      <div class="section-label">
        <span class="label-num">02</span>
        <span class="label-line"></span>
        <span class="label-text">Experience</span>
      </div>

      <h2 class="section-title">Where I've<br /><em>worked</em></h2>

      <div class="timeline">
        <div
          class="timeline-item"
          v-for="(job, i) in jobs"
          :key="i"
          :class="{ active: activeIndex === i }"
          @click="activeIndex = i"
        >
          <div class="timeline-left">
            <div class="timeline-dot"></div>
            <div class="timeline-connector" v-if="i < jobs.length - 1"></div>
          </div>

          <div class="timeline-content">
            <div class="job-header">
              <div>
                <h3 class="job-title">{{ job.role }}</h3>
                <p class="job-company">
                  {{ job.company }}
                  <span class="job-type">{{ job.type }}</span>
                </p>
              </div>
              <span class="job-period">{{ job.period }}</span>
            </div>

            <div class="job-body" v-show="activeIndex === i">
              <ul class="job-bullets">
                <li v-for="bullet in job.bullets" :key="bullet">
                  <span class="bullet-arrow">→</span>
                  {{ bullet }}
                </li>
              </ul>
              <div class="job-tags">
                <span class="tag" v-for="tag in job.tags" :key="tag">{{ tag }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const activeIndex = ref(0)

const jobs = [
  {
    role: 'Web Developer | Mobile App Developer (Front-End)',
    company: 'Infosoft',
    type: '· Full-time',
    period: '2024 — Present',
    bullets: [
      'Developed and maintained scalable web applications using Vue.js',
      'Built UI components using Vuetify for consistent and responsive design systems',
      'Integrated RESTful APIs to connect mobile apps and web with backend services',
      'Collaborated with designers and backend developers to deliver complete features',
      'Implemented authentication and security best practices for web applications',
      'Debugged and resolved technical issues to ensure system stability',
      'Designed reusable components to speed up development and maintain consistency',
      'Built dynamic dashboards and data visualizations (e.g., using charts like ApexCharts)',
      'Developed cross-platform mobile applications using React Native with Expo',
      'Handled device features such as camera, storage, and notifications via Expo APIs',
    ],
    tags: [
      'Vue2',
      'React Native',
      'TypeScript',
      'JavaScript',
      'Postman',
      'Bitbucket',
      'Vuetify',
      'Tailwind',
      'Nuxt2',
    ],
  },
  {
    role: 'Frontend Developer',
    company: 'Klan 3D Inc',
    type: 'Freelance',
    period: 'Sep 2024 — Dec 2024',
    bullets: [
      'Developed the user interface for Klan3D based on Figma mockups using Laravel Blade, ensuring pixel-perfect implementation',
      'Translated Figma designs into responsive web interfaces using Laravel Blade templates',
      'Built and maintained responsive UI for Klan3D, ensuring compatibility across multiple screen sizes and devices',
      'Collaborated with designers to accurately implement UI/UX from Figma into functional interfacess',
      'Optimized layouts and components to ensure consistency and responsiveness across different dimensions',
    ],
    tags: ['laravel', 'Blade', 'Github', 'tailwind'],
  },
  {
    role: 'Frontend Developer (Intern)',
    company: 'Infosoft.',
    type: '· Full-time',
    period: 'Feb 2024 — May 2024',
    bullets: [
      'Contributed to the development and maintenance of responsive web applications for an Australian client using Vue.js for dynamic interfaces',
      'Collaborated with the development team to build new features, fix bugs, and improve overall application performances',
      'Gained hands-on experience working with version control systems like Git in a collaborative development environment',
      'Ensured cross-browser and multi-device compatibility for a seamless user experience',
    ],
    tags: ['JavaScript', 'Vue', 'Tailwind', 'Bitbucket'],
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
  margin-bottom: 3rem;
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

.section-title {
  font-family: var(--font-display);
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 700;
  line-height: 1.05;
  margin-bottom: 4rem;
  letter-spacing: -0.02em;
}
.section-title em {
  font-style: italic;
  color: var(--accent);
}

.timeline {
  max-width: 800px;
}

.timeline-item {
  display: flex;
  gap: 2rem;
  cursor: pointer;
}

.timeline-left {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex-shrink: 0;
}

.timeline-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  border: 2px solid var(--text-muted);
  background: var(--bg);
  margin-top: 0.35rem;
  transition: all 0.3s;
  flex-shrink: 0;
}

.timeline-item.active .timeline-dot,
.timeline-item:hover .timeline-dot {
  border-color: var(--accent);
  background: var(--accent);
  box-shadow: 0 0 12px rgba(200, 169, 110, 0.4);
}

.timeline-connector {
  width: 1px;
  flex: 1;
  background: var(--border);
  margin: 0.5rem 0;
  min-height: 2rem;
}

.timeline-content {
  flex: 1;
  padding-bottom: 3rem;
}

.job-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 1.25rem;
}

.job-title {
  font-family: var(--font-display);
  font-size: 1.35rem;
  font-weight: 700;
  margin-bottom: 0.25rem;
  transition: color 0.3s;
}

.timeline-item:hover .job-title,
.timeline-item.active .job-title {
  color: var(--accent);
}

.job-company {
  font-size: 0.8rem;
  color: var(--text-muted);
}

.job-type {
  color: var(--accent);
  margin-left: 0.25rem;
}

.job-period {
  font-size: 0.72rem;
  color: var(--text-muted);
  letter-spacing: 0.05em;
  white-space: nowrap;
}

.job-body {
  animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-8px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.job-bullets {
  list-style: none;
  margin-bottom: 1.5rem;
}

.job-bullets li {
  display: flex;
  gap: 0.75rem;
  font-size: 0.875rem;
  color: var(--text-muted);
  padding: 0.4rem 0;
  line-height: 1.6;
}

.bullet-arrow {
  color: var(--accent);
  flex-shrink: 0;
  margin-top: 0.1rem;
}

.job-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tag {
  font-size: 0.65rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  border: 1px solid var(--border);
  color: var(--text-muted);
  padding: 0.3rem 0.75rem;
  transition: all 0.3s;
}

.tag:hover {
  border-color: var(--accent);
  color: var(--accent);
}
</style>
