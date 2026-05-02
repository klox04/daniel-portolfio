<template>
  <section id="projects" class="projects section-pad">
    <div class="container">
      <div class="section-label">
        <span class="label-num">03</span>
        <span class="label-line"></span>
        <span class="label-text">Projects</span>
      </div>

      <h2 class="section-title">Things I've<br /><em>built</em></h2>

      <p class="projects-note">
        <span class="note-icon">⚠</span>
        Some projects are under NDA — click to view details.
      </p>

      <div class="projects-grid">
        <article
          class="project-card"
          v-for="(project, i) in projects"
          :key="i"
          :class="{ featured: project.featured, clickable: project.nda }"
          @click="openModal(project)"
        >
          <div class="project-image">
            <div class="project-img-inner">
              <img
                v-if="project.images && project.images.length"
                :src="project.images[0]"
                :alt="project.title"
                class="screenshot"
              />
              <div v-else class="screenshot-placeholder">
                <div class="placeholder-lines">
                  <div class="ph-bar ph-bar-wide"></div>
                  <div class="ph-bar ph-bar-mid"></div>
                  <div class="ph-row">
                    <div class="ph-block"></div>
                    <div class="ph-block"></div>
                  </div>
                  <div class="ph-bar ph-bar-narrow"></div>
                </div>
                <p class="placeholder-label">Screenshot Preview</p>
              </div>
            </div>
            <div class="nda-badge" v-if="project.nda">
              <span>NDA · Click to view</span>
            </div>
            <div class="img-count-badge" v-if="project.images && project.images.length > 1">
              <span>⊞ {{ project.images.length }} screenshots</span>
            </div>
            <div class="project-num">{{ String(i + 1).padStart(2, '0') }}</div>
          </div>

          <div class="project-info">
            <div class="project-header">
              <h3 class="project-title">{{ project.title }}</h3>
              <div class="project-links">
                <a
                  v-if="project.demo"
                  :href="project.demo"
                  target="_blank"
                  class="project-link"
                  title="Live Demo"
                  @click.stop
                  >↗</a
                >
                <a
                  v-if="project.github"
                  :href="project.github"
                  target="_blank"
                  class="project-link"
                  title="GitHub"
                  @click.stop
                  >⌥</a
                >
              </div>
            </div>
            <p class="project-desc">{{ project.description }}</p>
            <div class="project-tags">
              <span class="tag" v-for="tag in project.tags" :key="tag">{{ tag }}</span>
            </div>
          </div>
        </article>
      </div>
    </div>

    <!-- Modal -->
    <Transition name="modal">
      <div class="modal-overlay" v-if="selectedProject" @click="closeModal">
        <div class="modal" @click.stop>
          <button class="modal-close" @click="closeModal">✕</button>

          <!-- Carousel -->
          <div class="modal-image">
            <template v-if="selectedProject.images && selectedProject.images.length">
              <Transition :name="slideDirection" mode="out-in">
                <img
                  :key="carouselIndex"
                  :src="selectedProject.images[carouselIndex]"
                  :alt="`${selectedProject.title} screenshot ${carouselIndex + 1}`"
                  class="modal-screenshot"
                />
              </Transition>

              <template v-if="selectedProject.images.length > 1">
                <button class="carousel-btn prev" @click.stop="prevSlide">&#8249;</button>
                <button class="carousel-btn next" @click.stop="nextSlide">&#8250;</button>

                <div class="carousel-dots">
                  <span
                    v-for="(_, i) in selectedProject.images"
                    :key="i"
                    class="carousel-dot"
                    :class="{ active: i === carouselIndex }"
                    @click.stop="goToSlide(i)"
                  ></span>
                </div>

                <div class="carousel-counter">
                  {{ carouselIndex + 1 }} / {{ selectedProject.images.length }}
                </div>
              </template>
            </template>

            <div v-else class="modal-no-image">
              <div class="placeholder-lines">
                <div class="ph-bar ph-bar-wide"></div>
                <div class="ph-bar ph-bar-mid"></div>
                <div class="ph-row">
                  <div class="ph-block"></div>
                  <div class="ph-block"></div>
                </div>
                <div class="ph-bar ph-bar-narrow"></div>
              </div>
              <p class="placeholder-label">Screenshot not available</p>
            </div>

            <div class="modal-nda-label" v-if="selectedProject.nda">
              <span>&#128274; Under NDA</span>
            </div>
          </div>

          <!-- Thumbnail strip -->
          <div
            class="modal-thumbs"
            v-if="selectedProject.images && selectedProject.images.length > 1"
          >
            <button
              v-for="(img, i) in selectedProject.images"
              :key="i"
              class="thumb"
              :class="{ active: i === carouselIndex }"
              @click="goToSlide(i)"
            >
              <img :src="img" :alt="`thumb ${i + 1}`" />
            </button>
          </div>

          <div class="modal-body">
            <h2 class="modal-title">{{ selectedProject.title }}</h2>
            <p class="modal-desc">{{ selectedProject.description }}</p>

            <div class="modal-section" v-if="selectedProject.highlights">
              <p class="modal-section-label">Highlights</p>
              <ul class="modal-highlights">
                <li v-for="h in selectedProject.highlights" :key="h">
                  <span>&#8594;</span> {{ h }}
                </li>
              </ul>
            </div>

            <div class="modal-section">
              <p class="modal-section-label">Tech Stack</p>
              <div class="modal-tags">
                <span class="tag" v-for="tag in selectedProject.tags" :key="tag">{{ tag }}</span>
              </div>
            </div>

            <p class="modal-nda-note" v-if="selectedProject.nda">
              This project is protected under a Non-Disclosure Agreement. Specific details, client
              name, and source code cannot be shared publicly.
            </p>
          </div>
        </div>
      </div>
    </Transition>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface Project {
  title: string
  description: string
  tags: string[]
  nda: boolean
  featured?: boolean
  images?: string[]
  demo?: string
  github?: string
  highlights?: string[]
}

const selectedProject = ref<Project | null>(null)
const carouselIndex = ref(0)
const slideDirection = ref('slide-left')

const openModal = (project: Project) => {
  selectedProject.value = project
  carouselIndex.value = 0
  document.body.style.overflow = 'hidden'
}

const closeModal = () => {
  selectedProject.value = null
  document.body.style.overflow = ''
}

const goToSlide = (i: number) => {
  slideDirection.value = i > carouselIndex.value ? 'slide-left' : 'slide-right'
  carouselIndex.value = i
}

const prevSlide = () => {
  const len = selectedProject.value?.images?.length ?? 1
  slideDirection.value = 'slide-right'
  carouselIndex.value = (carouselIndex.value - 1 + len) % len
}

const nextSlide = () => {
  const len = selectedProject.value?.images?.length ?? 1
  slideDirection.value = 'slide-left'
  carouselIndex.value = (carouselIndex.value + 1) % len
}

const projects: Project[] = [
  {
    title: 'Assistance Portal',
    description:
      'An assistance portal designed to streamline daily record management, replacing manual processes with a fully digital system to improve efficiency, accuracy, and ease of data handling for everyday operations.',
    tags: ['Vue', 'Laravel', 'PostgreSQL', 'Vuetify', 'Nuxt'],
    nda: true,
    featured: true,
    images: [
      '/image/image.png',
      '/image/camiguinayuada.png',
      '/image/ayuda1.png',
      '/image/ayuda2.png',
      '/image/ayuda3.png',
    ],
    highlights: [
      'Enable to sign a paper with e-esignature ',
      'Role-based access control for admin, supper admin, staff, governor and other deparment',
      'Custom reporting module with exportable PDF/Excel reports',
      'handle over 10,000+ daily data records and counting , ensuring scalable performance, reliability, and smooth processing even under heavy system load.',
    ],
  },
  {
    title: 'Camiguin System',
    description:
      'Built an admin-based rewards system with spin-the-wheel functionality, user and merchant management, QR code kiosk integration, real-time resident statistics, and a custom reporting module with PDF/Excel export.',
    tags: ['Nuxt', 'Vuetify', 'PostgreSQL', 'Vue', 'Laravel'],
    nda: true,
    featured: true,
    images: [
      '/image/projectimage.png',
      '/image/reward1.png',
      '/image/reward2.png',
      '/image/reward3.png',
      // '/image/crm-2.png',
    ],
    highlights: [
      'Enable administrators to create and manage a spin-the-wheel rewards system ',
      'Allow administrators to create user accounts and update/reset passwords',
      'Integrate QR code scanning via kiosk and monitor it by administrators',
      'Provide statistical dashboards to monitor total registered residents ',
      'Include a custom reporting module with exportable PDF and Excel reports',
      'Allow administrators to create and manage merchants for the rewards system',
    ],
  },
  {
    title: 'E-commerce Storefront',
    description:
      'A performant online store with cart, checkout flow, payment gateway integration, and admin inventory management.',
    tags: ['Nuxt 3', 'Stripe', 'Supabase', 'Tailwind'],
    nda: false,
    demo: 'https://your-demo-link.com',
    github: 'https://github.com/daniel/project',
    images: ['/image/barm2.png', '/image/barm1.png'],
  },
  {
    title: 'Booking System',
    description:
      'An appointment scheduling system with calendar sync, SMS/email reminders, and multi-staff management.',
    tags: ['Vue 3', 'Express', 'MySQL', 'Twilio'],
    nda: true,
    images: ['/image/registrar.png'],
    highlights: [
      'Google Calendar sync for real-time availability',
      'Automated SMS and email reminders via Twilio',
      'Multi-staff scheduling with conflict detection',
      'Client self-booking portal with rescheduling support',
    ],
  },
  {
    title: 'Portfolio Template',
    description:
      'An open-source developer portfolio built with Vue 3, TypeScript, and Tailwind CSS. Clean and customizable.',
    tags: ['Vue 3', 'TypeScript', 'Tailwind'],
    nda: false,
    github: 'https://github.com/daniel/portfolio',
    images: [],
  },
  {
    title: 'Internal HR Tool',
    description:
      'HR management tool covering employee records, leave requests, payroll summaries, and department reporting.',
    tags: ['Laravel', 'Vue 3', 'Livewire', 'Alpine.js'],
    nda: true,
    images: [],
    highlights: [
      'Employee records with document storage and history',
      'Leave request system with manager approval workflow',
      'Payroll summary reports per department and period',
      'Org chart visualization with role management',
    ],
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
  margin-bottom: 1.5rem;
  letter-spacing: -0.02em;
}
.section-title em {
  font-style: italic;
  color: var(--accent);
}

.projects-note {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  font-size: 0.78rem;
  color: var(--text-muted);
  margin-bottom: 4rem;
  padding: 0.75rem 1.25rem;
  border: 1px solid var(--border);
  width: fit-content;
}
.note-icon {
  color: var(--accent);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
  gap: 1.5rem;
}

.project-card {
  background: var(--bg-2);
  border: 1px solid var(--border);
  overflow: hidden;
  transition: all 0.3s;
  position: relative;
}
.project-card:hover {
  border-color: rgba(200, 169, 110, 0.4);
  transform: translateY(-4px);
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4);
}
.project-card.clickable {
  cursor: pointer;
}
.project-card.clickable:hover .nda-badge {
  background: var(--accent);
  color: var(--bg);
}

.project-image {
  position: relative;
  aspect-ratio: 16/9;
  overflow: hidden;
  background: var(--bg-3);
}
.project-img-inner {
  width: 100%;
  height: 100%;
}
.screenshot {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}
.project-card:hover .screenshot {
  transform: scale(1.04);
}

.screenshot-placeholder {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1.5rem;
  background: var(--bg-3);
  padding: 2rem;
}
.placeholder-lines {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}
.ph-bar {
  height: 8px;
  background: rgba(200, 169, 110, 0.12);
  border-radius: 2px;
}
.ph-bar-wide {
  width: 100%;
}
.ph-bar-mid {
  width: 72%;
}
.ph-bar-narrow {
  width: 50%;
}
.ph-row {
  display: flex;
  gap: 0.6rem;
  margin: 0.4rem 0;
}
.ph-block {
  height: 50px;
  flex: 1;
  background: rgba(200, 169, 110, 0.08);
  border-radius: 2px;
}
.placeholder-label {
  font-size: 0.65rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--text-muted);
  opacity: 0.5;
}

.nda-badge {
  position: absolute;
  top: 0.75rem;
  left: 0.75rem;
  background: rgba(10, 10, 10, 0.85);
  border: 1px solid var(--accent);
  color: var(--accent);
  font-size: 0.6rem;
  letter-spacing: 0.15em;
  padding: 0.2rem 0.6rem;
  transition: all 0.3s;
}
.img-count-badge {
  position: absolute;
  top: 0.75rem;
  right: 0.75rem;
  background: rgba(10, 10, 10, 0.85);
  border: 1px solid var(--border);
  color: var(--text-muted);
  font-size: 0.6rem;
  letter-spacing: 0.1em;
  padding: 0.2rem 0.6rem;
}
.project-num {
  position: absolute;
  bottom: 0.75rem;
  right: 0.75rem;
  font-family: var(--font-display);
  font-size: 3rem;
  font-weight: 900;
  color: rgba(200, 169, 110, 0.1);
  line-height: 1;
  pointer-events: none;
}

.project-info {
  padding: 1.5rem;
}
.project-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 0.75rem;
}
.project-title {
  font-family: var(--font-display);
  font-size: 1.2rem;
  font-weight: 700;
}
.project-links {
  display: flex;
  gap: 0.5rem;
}
.project-link {
  width: 30px;
  height: 30px;
  border: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.85rem;
  color: var(--text-muted);
  transition: all 0.3s;
}
.project-link:hover {
  border-color: var(--accent);
  color: var(--accent);
}
.project-desc {
  font-size: 0.825rem;
  color: var(--text-muted);
  line-height: 1.7;
  margin-bottom: 1.25rem;
}
.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
}
.tag {
  font-size: 0.62rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  border: 1px solid var(--border);
  color: var(--text-muted);
  padding: 0.25rem 0.6rem;
}

/* Modal */
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.85);
  backdrop-filter: blur(6px);
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1.5rem;
}
.modal {
  background: var(--bg-2);
  border: 1px solid var(--border);
  width: 100%;
  max-width: 720px;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
}
.modal-close {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: rgba(10, 10, 10, 0.8);
  border: 1px solid var(--border);
  color: var(--text-muted);
  width: 32px;
  height: 32px;
  cursor: pointer;
  font-size: 0.75rem;
  z-index: 10;
  transition: all 0.2s;
}
.modal-close:hover {
  border-color: var(--accent);
  color: var(--accent);
}

/* Carousel */
.modal-image {
  position: relative;
  aspect-ratio: 16/9;
  background: var(--bg-3);
  overflow: hidden;
}
.modal-screenshot {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(10, 10, 10, 0.75);
  border: 1px solid rgba(200, 169, 110, 0.3);
  color: var(--text);
  width: 40px;
  height: 40px;
  font-size: 1.5rem;
  cursor: pointer;
  z-index: 5;
  transition: all 0.2s;
  display: flex;
  align-items: center;
  justify-content: center;
}
.carousel-btn:hover {
  border-color: var(--accent);
  color: var(--accent);
}
.carousel-btn.prev {
  left: 0.75rem;
}
.carousel-btn.next {
  right: 0.75rem;
}

.carousel-dots {
  position: absolute;
  bottom: 0.85rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 0.45rem;
  z-index: 5;
}
.carousel-dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.25);
  cursor: pointer;
  transition: all 0.25s;
  border: none;
  display: inline-block;
}
.carousel-dot.active {
  background: var(--accent);
  transform: scale(1.35);
}

.carousel-counter {
  position: absolute;
  top: 0.75rem;
  right: 3rem;
  background: rgba(10, 10, 10, 0.75);
  color: var(--text-muted);
  font-size: 0.65rem;
  letter-spacing: 0.1em;
  padding: 0.2rem 0.6rem;
}

/* Thumbnails */
.modal-thumbs {
  display: flex;
  gap: 0.5rem;
  padding: 0.75rem;
  background: var(--bg-3);
  overflow-x: auto;
  border-bottom: 1px solid var(--border);
}
.thumb {
  flex-shrink: 0;
  width: 72px;
  height: 48px;
  border: 2px solid transparent;
  cursor: pointer;
  overflow: hidden;
  transition: border-color 0.2s;
  background: none;
  padding: 0;
}
.thumb img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}
.thumb.active {
  border-color: var(--accent);
}
.thumb:hover {
  border-color: rgba(200, 169, 110, 0.5);
}

.modal-nda-label {
  position: absolute;
  bottom: 1rem;
  left: 1rem;
  background: rgba(10, 10, 10, 0.9);
  border: 1px solid var(--accent);
  color: var(--accent);
  font-size: 0.65rem;
  letter-spacing: 0.12em;
  padding: 0.3rem 0.75rem;
}

.modal-no-image {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1.5rem;
  padding: 2rem;
}

.modal-body {
  padding: 2rem;
}
.modal-title {
  font-family: var(--font-display);
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: 0.75rem;
}
.modal-desc {
  font-size: 0.9rem;
  color: var(--text-muted);
  line-height: 1.8;
  margin-bottom: 1.75rem;
}
.modal-section {
  margin-bottom: 1.75rem;
}
.modal-section-label {
  font-size: 0.65rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 0.75rem;
}
.modal-highlights {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}
.modal-highlights li {
  display: flex;
  gap: 0.75rem;
  font-size: 0.85rem;
  color: var(--text-muted);
  line-height: 1.6;
}
.modal-highlights li span {
  color: var(--accent);
  flex-shrink: 0;
}
.modal-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}
.modal-nda-note {
  font-size: 0.75rem;
  color: var(--text-muted);
  opacity: 0.6;
  padding-top: 1.5rem;
  border-top: 1px solid var(--border);
  line-height: 1.7;
}

/* Slide transitions */
.slide-left-enter-active,
.slide-left-leave-active,
.slide-right-enter-active,
.slide-right-leave-active {
  transition: all 0.3s ease;
  position: absolute;
  width: 100%;
  height: 100%;
}
.slide-left-enter-from {
  transform: translateX(100%);
  opacity: 0;
}
.slide-left-leave-to {
  transform: translateX(-100%);
  opacity: 0;
}
.slide-right-enter-from {
  transform: translateX(-100%);
  opacity: 0;
}
.slide-right-leave-to {
  transform: translateX(100%);
  opacity: 0;
}

/* Modal transition */
.modal-enter-active,
.modal-leave-active {
  transition: all 0.3s ease;
}
.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}
.modal-enter-from .modal,
.modal-leave-to .modal {
  transform: translateY(20px) scale(0.97);
}

@media (max-width: 768px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
  .carousel-btn {
    width: 32px;
    height: 32px;
    font-size: 1.1rem;
  }
}
</style>
