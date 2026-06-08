<template>
  <section id="contact" class="contact">

   

      <!-- Left panel -->
      <div class="panel-left">
        <div class="panel-left-inner">
          <h2 class="section-heading">Contact</h2>

          <div class="info-list">
            <div class="info-row">
              <span class="info-icon-wrap" aria-hidden="true">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="4" width="20" height="16" rx="2"/><path d="m2 7 10 7 10-7"/></svg>
              </span>
              <span class="info-text">{{ contact.email }}</span>
            </div>

            <div class="info-row">
              <span class="info-icon-wrap" aria-hidden="true">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07A19.5 19.5 0 0 1 4.1 11.73 19.79 19.79 0 0 1 1 3.19 2 2 0 0 1 2.98 1h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L7.09 8.91a16 16 0 0 0 5.91 5.91l1.27-1.27a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 21 16z"/></svg>
              </span>
              <span class="info-text">{{ contact.phone }}</span>
            </div>

            <div class="info-row info-row--static">
              <span class="info-icon-wrap" aria-hidden="true">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/><circle cx="12" cy="10" r="3"/></svg>
              </span>
              <span class="info-text">{{ contact.location }}</span>
            </div>
          </div>
        </div>
      </div>


   
  </section>
</template>

<script>
export default {
  name: 'ContactSection',
  props: {
    contact: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      sent: false,
      form: { name: '', email: '', subject: '', message: '' }
    };
  },
  methods: {
    handleSubmit() {
      console.log('Form submitted:', this.form);
      this.sent = true;
      this.form = { name: '', email: '', subject: '', message: '' };
      setTimeout(() => { this.sent = false; }, 3000);
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;1,300&family=Outfit:wght@300;400;500&display=swap');

/* ── Variables ── */
.contact {
  --purple-a: #667eea;
  --purple-b: #764ba2;
  --purple-mid: #6e5bbd;
  --fg: #1a1625;
}

/* ── Section ── */
.contact {
  font-family: 'Outfit', sans-serif;
  color: var(--fg);
  min-height: 100vh;
}

/* ── Full Width Panel ── */
.panel-left {
  background: linear-gradient(145deg, var(--purple-a) 0%, var(--purple-b) 100%);
  min-height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 5rem 2rem;
  position: relative;
  overflow: hidden;
}

.panel-left::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(255,255,255,0.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.05) 1px, transparent 1px);
  background-size: 48px 48px;
}

.panel-left-inner {
  position: relative;
  z-index: 1;
  width: 100%;
  max-width: 800px;
  text-align: center;
}

/* ── Typography ── */
.section-tag {
  display: inline-block;
  font-size: 0.65rem;
  font-weight: 500;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.5);
  border: 1px solid rgba(255,255,255,0.15);
  padding: 4px 12px;
  border-radius: 100px;
  margin-bottom: 1.75rem;
}

.section-heading {
  font-family: 'Cormorant Garamond', serif;
  font-size: clamp(3rem, 6vw, 5rem);
  font-weight: 300;
  line-height: 1.1;
  color: #fff;
  margin: 0 0 1.5rem;
}

.section-heading em {
  font-style: italic;
  color: rgba(255,255,255,0.75);
}

.section-sub {
  font-size: 1rem;
  line-height: 1.8;
  color: rgba(255,255,255,0.65);
  max-width: 650px;
  margin: 0 auto 3rem;
}

/* ── Contact Info ── */
.info-list {
  max-width: 600px;
  margin: 0 auto;
  border-top: 1px solid rgba(255,255,255,0.1);
}

.info-row {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 1.2rem 0;
  border-bottom: 1px solid rgba(255,255,255,0.1);
  text-decoration: none;
  color: rgba(255,255,255,0.8);
  transition: all 0.25s ease;
}

.info-row:hover {
  color: #fff;
}

.info-row:hover .info-arrow {
  transform: translate(2px, -2px);
}

.info-icon-wrap {
  width: 40px;
  height: 40px;
  border-radius: 10px;
  background: rgba(255,255,255,0.1);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.info-text {
  flex: 1;
  text-align: left;
}

.info-arrow {
  color: rgba(255,255,255,0.4);
  transition: transform 0.2s ease;
}

.info-row--static {
  cursor: default;
}

/* ── Mobile ── */
@media (max-width: 768px) {
  .panel-left {
    padding: 4rem 1.5rem;
  }

  .section-heading {
    font-size: 3rem;
  }

  .info-text {
    font-size: 0.9rem;
  }
}
</style>