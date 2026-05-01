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
    role: 'Full-Stack Developer',
    company: 'Tech Company',
    type: '· Full-time',
    period: '2023 — Present',
    bullets: [
      'Built and maintained multiple web applications using Vue 3 and Laravel',
      'Designed and implemented RESTful APIs consumed by mobile and web clients',
      'Collaborated closely with design team to deliver pixel-perfect UI components',
      'Improved application performance by 40% through code refactoring and caching',
    ],
    tags: ['Vue 3', 'Laravel', 'TypeScript', 'PostgreSQL'],
  },
  {
    role: 'Frontend Developer',
    company: 'Digital Agency',
    type: '· Contract',
    period: '2022 — 2023',
    bullets: [
      'Developed responsive landing pages and web apps for various clients',
      'Integrated third-party APIs and payment gateways',
      'Maintained and improved existing React codebases',
      'Worked in an agile team with weekly sprints and code reviews',
    ],
    tags: ['React', 'Next.js', 'Tailwind CSS', 'REST APIs'],
  },
  {
    role: 'Junior Web Developer',
    company: 'Startup Inc.',
    type: '· Full-time',
    period: '2021 — 2022',
    bullets: [
      'Assisted in building an e-commerce platform from scratch',
      'Wrote clean, reusable HTML/CSS/JS components',
      'Learned and applied version control workflows using Git',
      'Participated in daily standups and delivered features on schedule',
    ],
    tags: ['HTML', 'CSS', 'JavaScript', 'PHP'],
  },
]
</script>

<style scoped>
.section-pad { padding: 8rem 2rem; }
.container { max-width: 1200px; margin: 0 auto; }

.section-label {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 3rem;
}
.label-num { font-size: 0.7rem; color: var(--accent); letter-spacing: 0.1em; }
.label-line { flex: 0 0 60px; height: 1px; background: var(--border); }
.label-text { font-size: 0.7rem; letter-spacing: 0.2em; text-transform: uppercase; color: var(--text-muted); }

.section-title {
  font-family: var(--font-display);
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 700;
  line-height: 1.05;
  margin-bottom: 4rem;
  letter-spacing: -0.02em;
}
.section-title em { font-style: italic; color: var(--accent); }

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
  box-shadow: 0 0 12px rgba(200,169,110,0.4);
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
  from { opacity: 0; transform: translateY(-8px); }
  to { opacity: 1; transform: translateY(0); }
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