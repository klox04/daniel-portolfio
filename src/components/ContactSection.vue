<template>
  <section id="contact" class="contact section-pad">
    <div class="container">
      <div class="section-label">
        <span class="label-num">04</span>
        <span class="label-line"></span>
        <span class="label-text">Contact</span>
      </div>

      <div class="contact-grid">
        <div class="contact-left">
          <h2 class="section-title">Let's work<br /><em>together</em></h2>
          <p class="contact-desc">
            I'm currently open to new opportunities. Whether you have a project in mind or just want
            to say hello — my inbox is always open.
          </p>

          <div class="contact-links">
            <a
              v-for="link in contactLinks"
              :key="link.label"
              :href="link.href"
              target="_blank"
              class="contact-link"
            >
              <span class="link-icon">{{ link.icon }}</span>
              <div>
                <p class="link-label">{{ link.label }}</p>
                <p class="link-value">{{ link.value }}</p>
              </div>
              <span class="link-arrow">↗</span>
            </a>
          </div>
        </div>

        <div class="contact-right">
          <form class="contact-form" @submit.prevent="handleSubmit">
            <div class="form-group">
              <label>Name</label>
              <input v-model="form.name" type="text" placeholder="Your name" required />
            </div>
            <div class="form-group">
              <label>Email</label>
              <input v-model="form.email" type="email" placeholder="your@email.com" required />
            </div>
            <div class="form-group">
              <label>Message</label>
              <textarea
                v-model="form.message"
                rows="5"
                placeholder="Tell me about your project..."
                required
              ></textarea>
            </div>
            <button type="submit" class="btn-submit">
              {{ submitted ? '✓ Message Sent' : 'Send Message' }}
            </button>
          </form>
        </div>
      </div>
    </div>

    <footer class="footer">
      <p>Designed & built by <span>Daniel</span> · {{ new Date().getFullYear() }}</p>
    </footer>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const submitted = ref(false)
const form = {
  email: '',
  name: '',
  message: '',
}
// const form = reactive({
//   name: '',
//   email: '',
//   message: '',
// })

const handleSubmit = () => {
  // Connect to your email service here (e.g. EmailJS, Formspree)
  console.log('Form submitted:', form)
  submitted.value = true
  setTimeout(() => (submitted.value = false), 3000)
}

const contactLinks = [
  {
    icon: '✉',
    label: 'Email',
    value: 'daniel@email.com',
    href: 'mailto:daniel@email.com',
  },
  {
    icon: '⌥',
    label: 'GitHub',
    value: 'github.com/daniel',
    href: 'https://github.com',
  },
  {
    icon: '◈',
    label: 'LinkedIn',
    value: 'linkedin.com/in/daniel',
    href: 'https://linkedin.com',
  },
]
</script>

<style scoped>
.section-pad {
  padding: 8rem 2rem 4rem;
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

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 6rem;
  align-items: start;
}

.contact-desc {
  color: var(--text-muted);
  font-size: 0.95rem;
  margin-bottom: 3rem;
  line-height: 1.8;
}

.contact-links {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.contact-link {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem 1.25rem;
  border: 1px solid var(--border);
  transition: all 0.3s;
  group: true;
}

.contact-link:hover {
  border-color: rgba(200, 169, 110, 0.4);
  background: rgba(200, 169, 110, 0.04);
}

.link-icon {
  font-size: 1.1rem;
  color: var(--accent);
  flex-shrink: 0;
}

.link-label {
  font-size: 0.65rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--text-muted);
}

.link-value {
  font-size: 0.85rem;
  color: var(--text);
  margin-top: 0.1rem;
}

.link-arrow {
  margin-left: auto;
  color: var(--text-muted);
  transition: color 0.3s;
}

.contact-link:hover .link-arrow {
  color: var(--accent);
}

/* Form */
.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.form-group label {
  font-size: 0.65rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--text-muted);
}

.form-group input,
.form-group textarea {
  background: var(--bg-2);
  border: 1px solid var(--border);
  color: var(--text);
  font-family: var(--font-mono);
  font-size: 0.875rem;
  padding: 0.85rem 1rem;
  outline: none;
  transition: border-color 0.3s;
  resize: vertical;
}

.form-group input:focus,
.form-group textarea:focus {
  border-color: rgba(200, 169, 110, 0.5);
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: var(--text-muted);
  opacity: 0.5;
}

.btn-submit {
  background: var(--accent);
  color: var(--bg);
  border: none;
  padding: 1rem 2rem;
  font-family: var(--font-mono);
  font-size: 0.75rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  cursor: pointer;
  transition: all 0.3s;
  align-self: flex-start;
}

.btn-submit:hover {
  background: var(--accent-2);
}

.footer {
  max-width: 1200px;
  margin: 6rem auto 0;
  padding: 2rem;
  border-top: 1px solid var(--border);
  font-size: 0.72rem;
  color: var(--text-muted);
  letter-spacing: 0.1em;
}

.footer span {
  color: var(--accent);
}

@media (max-width: 900px) {
  .contact-grid {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
}
</style>
